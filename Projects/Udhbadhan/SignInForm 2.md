```js
'use client';

import { useApiRequest } from '@/hooks/useApiRequest';

import useAuthStore from '@/lib/store/authStore'; // Zustand store

import { successTheme } from '@/styles/toastThemes';

import Cookies from 'js-cookie';

import { jwtDecode } from 'jwt-decode';

import { useRouter } from 'next/navigation';

import { useEffect, useState } from 'react';

import { useForm } from 'react-hook-form';

import toast from 'react-hot-toast';

import { BiBook, BiMessageAltError } from 'react-icons/bi';

import { FiBell } from 'react-icons/fi';

import { GoKey } from 'react-icons/go';

import { IoFileTrayFullOutline } from 'react-icons/io5';

import { LuSettings2 } from 'react-icons/lu';

import { MdOutlineLiveHelp } from 'react-icons/md';

  

interface LoginFormValues {

  username: string;

  password: string;

}

  

interface UserRole {

  _id: string;

  name: string;

  permissions: string[];

  description: string;

}

  

const SignInForm = () => {

  const {

    register,

    handleSubmit,

    formState: { errors },

    reset,

  } = useForm<LoginFormValues>();

  const router = useRouter();

  const setUser = useAuthStore((state) => state.setUser); // Zustand method to set user

  const [userIP, setUserIP] = useState(null);

  const device = typeof window !== 'undefined' ? window.navigator.userAgent : null;

  const dateTime = new Date();

  const formattedDateTime = dateTime.toISOString();

  

  // Initialize the useApiRequest hook for the login request

  const {

    data: loginResponse,

    error: loginError,

    executeWithoutToken: executeLogin,

  } = useApiRequest({

    endpoint: '/users/login',

    method: 'POST',

  });

  

  // Initialize the useApiRequest hook for Login history

  const {

    data: loginHistoryResponse,

    error: loginHistoryError,

    status,

    executeWithToken: executeLoginHistoryRequest,

  } = useApiRequest({

    endpoint: '/login-history/create',

    method: 'POST',

  });

  

  const onSubmit = async (formData: LoginFormValues) => {

    try {

      await executeLogin(formData); // Trigger login API call

    } catch (err) {

      console.error('Login failed:', err);

    }

  };

  

  useEffect(() => {

    fetch('https://api.ipify.org/?format=json')

      .then((response) => response.json())

      .then((data) => setUserIP(data?.ip))

      .catch((error) => console.error(error));

  }, []);

  

  const redirectToAppropriateRoute = (userRole: UserRole, router: any, reset: any) => {

    // Define all routes

    const allRoutes = [

      {

        path: '/admin_panel/document_management',

        title: 'Document Management',

        icon: <IoFileTrayFullOutline />,

        permission: 'document_management',

        iconClasses: 'text-[15px] font-bold text-gray-500 lg:text-[16px] xl:text-[20px]',

      },

      {

        path: '/admin_panel/dictionary',

        title: 'Dictionary',

        icon: <BiBook />,

        permission: 'library_management',

        iconClasses: 'text-[15px] font-bold text-gray-500 lg:text-[16px] xl:text-[20px]',

      },

      {

        path: '/admin_panel/system_settings',

        title: 'System Settings',

        icon: <LuSettings2 />,

        permission: 'system_setting_management',

        iconClasses: 'text-[17px] font-bold text-gray-500 lg:text-lg xl:text-[22px]',

      },

      {

        path: '/admin_panel/notification_management',

        title: 'Notification Management',

        icon: <FiBell />,

        permission: 'notification_management',

        iconClasses: 'text-[15px] font-bold text-gray-500 lg:text-[17px] xl:text-[20px]',

      },

      {

        path: '/admin_panel/usage_statistics',

        title: 'Usage Statistics',

        icon: <BiMessageAltError />,

        permission: 'usage_statistics_management',

        iconClasses: 'text-[16px] font-bold text-gray-500 lg:text-lg xl:text-[22px]',

      },

      {

        path: '/admin_panel/help_desk',

        title: 'Help Desk and Support',

        icon: <MdOutlineLiveHelp />,

        permission: 'help_disk_and_support_route_management',

        iconClasses: 'text-[17px] font-bold text-gray-500 lg:text-lg xl:text-[22px]',

      },

      {

        path: '/admin_panel/access_control',

        title: 'Access Control',

        icon: <GoKey />,

        permission: 'access_control_management',

        iconClasses: 'text-[15px] font-bold text-gray-500 lg:text-[17px] xl:text-[20px]',

      },

    ];

  

    // Check if the user is admin or super_admin

    if (['admin', 'super_admin'].includes(userRole.name)) {

      reset();

      router.push(allRoutes[0].path); // Redirect to the first route for admins or super admins

      return;

    }

  

    // Find a route with a matching permission from the user's role

    for (const route of allRoutes) {

      if (userRole.permissions.includes(route.permission)) {

        reset();

        router.push(route.path); // Redirect to the route with the matching permission

        return;

      }

    }

  

    // If no permission is found, redirect to a default route (e.g., /tools)

    reset();

    router.push('/tools');

  };

  

  /* ---------------Login Success Message and Additional API Request -------------- */

  useEffect(() => {

    if (loginResponse?.success) {

      toast.success(loginResponse?.message, successTheme);

      const token = loginResponse?.data?.accessToken;

      const userData = jwtDecode(token);

      setUser({ ...userData, token }); // Save user in Zustand

  

      // Store user data in a cookie for middleware access

      Cookies.set('user_UDB', JSON.stringify(userData), { path: '/' });

  

      const userId = userData && (userData as { _id: string })._id;

      if (userId) {

        // Trigger second API request after login is successful

        executeLoginHistoryRequest({

          userId: userId,

          loginTime: formattedDateTime,

          ipAddress: userIP,

          deviceInfo: device,

          loginMethod: 'email, password',

        })

          .then(() => {

            // After the second request, you can redirect or handle more logic

            const userRole = (

              userData as {

                role: {

                  _id: string;

                  name: string;

                  permissions: string[];

                  description: string;

                };

              }

            ).role;

            console.log('userRole: ', userRole);

            redirectToAppropriateRoute(userRole, router, reset);

          })

          .catch((err) => {

            console.error('Login History failed:', err);

          });

      }

    }

  }, [loginResponse, reset]);

  

  /* --------------Login Error Message----------- */

  useEffect(() => {

    if (

      loginError &&

      typeof loginError === 'object' &&

      'response' in loginError &&

      loginError.response &&

      typeof loginError.response === 'object' &&

      'data' in loginError.response &&

      loginError.response.data &&

      typeof loginError.response.data === 'object' &&

      'message' in loginError.response.data

    ) {

      const errorMessage = (loginError as { response: { data: { message: string } } }).response.data.message;

      toast.error(errorMessage);

    }

  }, [loginError]);

  

  return (

    <div>

      <form onSubmit={handleSubmit(onSubmit)}>

        <div className="mb-5">

          <input

            {...register('username', { required: 'Username is required' })}

            placeholder="Username"

            className="authInput"

          />

          {errors.username && <p className="authError">{errors.username.message}</p>}

        </div>

  

        <div className="mb-5">

          <input

            {...register('password', { required: 'Password is required' })}

            type="password"

            placeholder="Password"

            className="authInput"

          />

          {errors.password && <p className="authError">{errors.password.message}</p>}

        </div>

  

        <div className="mt-3 flex items-center justify-center">

          <button

            disabled={status === 'pending'}

            type="submit"

            className={`mx-auto w-[185px] ${status === 'pending' ? 'bg-orange-600' : 'bg-webPrimary'} p-2 text-white hover:bg-orange-600`}

          >

            {status === 'pending' ? ' Sign In...' : ' Sign In'}

          </button>

        </div>

      </form>

      <>

        <p className="border-b border-black py-8 text-center">

          By continuing, you agree to Udbhodans <span className="font-bold">conditions of use</span> and{' '}

          <span className="font-bold">privacy notice</span>.

        </p>

  

        <div className="mt-6 text-center">

          <span>Forget Password? </span>

          <span

            onClick={() => router.push('/forget-password')}

            className="cursor-pointer text-[#F87F18] hover:underline"

          >

            Rest Password

          </span>

        </div>

      </>

    </div>

  );

};

  

export default SignInForm;
```