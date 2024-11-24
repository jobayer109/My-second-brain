```js
'use client';
 
import { useEffect, useState } from 'react';

interface TroubleshootingTip {
  id: number;
  title: string;
  steps: string[];
}

const tips: TroubleshootingTip[] = [
  {
    id: 1,
    title: 'Unable to Log In',
    steps: [
      'Check Credentials: Ensure that you are entering the correct email and password. Remember that passwords are case-sensitive.',
      "Reset Password: If you've forgotten your password, click on the 'Forgot Password?' link on the login page to reset it.",
      'Account Deactivated: If your account has been deactivated by an admin, contact them to reactivate it.',
    ],
  },
  {
    id: 2,
    title: 'Document Upload Failures',
    steps: [
      'File Format: Ensure that the document is in an accepted format (e.g., PDF, DOCX, TXT). Check the file extension.',
      'File Size: Verify that the file does not exceed the maximum upload limit set by the system.',
      'Internet Connection: Ensure you have a stable internet connection before attempting to upload.',
    ],
  },
  {
    id: 3,
    title: 'Notifications Not Received',
    steps: [
      'Check Spam/Junk Folder: Sometimes, notification emails may land in the spam or junk folder.',
      'Notification Settings: Ensure that your notification preferences are correctly set up in the Notification Management section.',
      'Email Address: Verify that the correct email address is associated with your account.',
    ],
  },
];
  

const highlightText = (text: string, query: string) => {
  if (!query) return text;
  const escapedQuery = query.replace(/[-\/\\^$*+?.()|[\]{}]/g, '\\$&'); // Escape special characters
  const regex = new RegExp(`(${escapedQuery})`, 'gi'); // Match text (case-insensitive)
  return text.replace(regex, '<span class="bg-orange-200">$1</span>'); // Add highlight tag
};


const HighlightedText = ({ text, query }: { text: string; query: string }) => {
  const highlightedText = highlightText(text, query);
  return <span dangerouslySetInnerHTML={{ __html: highlightedText }} />;
};

export default function TroubleshootingTips() {
  const [searchQuery, setSearchQuery] = useState('');
  const [debouncedQuery, setDebouncedQuery] = useState('');
  
  // Debouncing the search query to avoid filtering on every keystroke
  useEffect(() => {
    const timeoutId = setTimeout(() => {
      setDebouncedQuery(searchQuery);
    }, 500);
  
    return () => clearTimeout(timeoutId); // Clean up timeout on unmount or change
  }, [searchQuery]);
  
  const filteredTips = tips.filter((tip) => {
    const searchLower = debouncedQuery.toLowerCase();
    return (
      tip.title.toLowerCase().includes(searchLower) ||
      tip.steps.some((step) => step.toLowerCase().includes(searchLower))
    );
  });
  

  return (
    <div>
      <div className="flexBetween mb-10">
        <h1 className="text-[24px] font-medium text-gray-900">Troubleshooting Tips</h1>
        <div className="relative">
          <input
            type="text"
            className="w-[309px] rounded-md border border-gray-200 bg-gray-50 py-2 pl-10 pr-4 focus:border-transparent focus:outline-none focus:ring-2 focus:ring-[#ffeacf]"
            placeholder="Search for tips"
            value={searchQuery}
            onChange={(e) => setSearchQuery(e.target.value)}
          />
          <svg
            className="absolute left-3 top-1/2 -translate-y-1/2 text-gray-400"
            width="16"
            height="16"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            strokeWidth="2"
            strokeLinecap="round"
            strokeLinejoin="round"
          >
            <circle cx="11" cy="11" r="8" />
            <line x1="21" y1="21" x2="16.65" y2="16.65" />
          </svg>
        </div>
      </div>
      
      <div className="flex flex-col space-y-10 px-6">
        {filteredTips.length > 0 ? (
          <div className="grid gap-x-12 gap-y-8 md:grid-cols-2">
            {filteredTips.map((tip) => (
              <div key={tip.id} className="space-y-4">
                <h2 className="flex items-baseline gap-2">
                  <span className="font-medium">{tip.id}.</span>
                  <HighlightedText text={tip.title} query={debouncedQuery} />
                </h2>
                <ul className="list-disc space-y-3 pl-6">
                  {tip.steps.map((step, index) => (
                    <li key={index} className="text-sm leading-relaxed text-gray-600">
                      <HighlightedText text={step} query={debouncedQuery} />
                    </li>
                  ))}
                </ul>
              </div>
            ))}
          </div>
        ) : (
          <p className="text-center text-gray-600">No results found for your search.</p>
        )}
      </div>
    </div>
  );
}
```

