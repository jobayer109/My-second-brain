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

    const adminRoutes = {

      user_roles_and_permissions: '/admin_panel/',

      user_accounts: '/admin_panel/user_accounts',

      document_management: '/admin_panel/document_management',

      dictionary: '/admin_panel/dictionary',

      system_settings: '/admin_panel/system_settings',

      notification_management: '/admin_panel/notification_management',

      usage_statistics: '/admin_panel/usage_statistics',

      help_desk: '/admin_panel/help_desk',

      access_control: '/admin_panel/access_control',

    };

  

    const toolsRoutes = {

      proofreading: '/tools/',

      ocr: '/tools/ocr',

      paraphraser: '/tools/paraphraser',

      generate_reference: '/tools/generate_reference',

    };

  

    const allRoutes = { ...adminRoutes, ...toolsRoutes };

    console.log('allRoutes: ', allRoutes);

  

    if (['admin', 'super_admin'].includes(userRole.name)) {

      reset();

      router.push(adminRoutes.user_roles_and_permissions);

      return;

    } else {

      router.push(toolsRoutes.proofreading);

    }

  

    const firstAccessibleRoute = userRole.permissions.find((permission) => Object.keys(allRoutes).includes(permission));

  

    console.log('firstAccessibleRoute: ', firstAccessibleRoute);

  

    if (firstAccessibleRoute) {

      reset();

      router.push(allRoutes[firstAccessibleRoute as keyof typeof allRoutes]);

    } else {

      reset();

      router.push('/tools');

    }

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