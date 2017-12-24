
## Deploying App created with create-react-app

Steps:

1. Check and adjust basepath
   <BrowserRouter basename="/my-app/"> 
   This is always required when you're serving your app from other than the root domain. So for example, if you're serving your app from 
   www.example.com/my-app, then you need to set the basename as above.
   
2. Build and Optimize Project
   npm run build 
   You'll see a folder that contains optimized production build. See build folder.
   
3. Server must ALWAYS serve index.html (also for 404 cases)

4. Upload Build Artifacts (from step 2) to (static) server 
