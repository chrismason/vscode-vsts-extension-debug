# vscode-vsts-extension-debug
Sample project to show debugging a VSTS extension with VS Code

# Getting started
- Install VS Code from [https://code.visualstudio.com/](here)
- Install the "Debugger for Chrome" extension from [https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome](here) 
- Install NodeJS from [https://nodejs.org](here)
- Clone this repository
- Create a publisher at the [VSTS marketplace](https://marketplace.visualstudio.com/manage)
- Insert your publisher ID in `configs/dev.json` and `configs/release.json`
- Choose an ID for your extension and insert it in `vss-extension.json`
- Run `npm install`

# Developing & debugging
## Publishing a development version of your extension
First, you'll need to publish & install a development version of your extension. This will load the extension content from your local machine, making development & debugging a whole lot easier.
This is a one-time action. Only if you update the extension manifest (`vss-extension.json`) you will need to re-run these steps.
- Run `npm run publish:dev`
- Upload the resulting `.vsix` file to the VSTS marketplace and share it with your account
- Navigate to your VSTS account and go to "Manage Extensions"
- Install the extension in your account

## Running a development instance
- Run `npm run dev`
- Open Chrome and navigate to [https://localhost:3000](https://localhost:3000)
- You'll see a warning about your connection not being private. This is because we're using a self-signed certificate on our local dev server
- Click "Advanced" and then "Proceed to localhost"
- Now go to your VSTS account. You should have a "Demo" hub under the "Home" hub group in all of your Team Projects. When you open the "Demo" hub, you'll see a nice personal welcome message.

## Debugging from VS Code
- Make sure that `npm run dev` is still running
- Set some breakpoints in the TypeScript code in VS Code
- Start a debugging session (hit F5)
- Chrome will launch, directing you to [https://localhost:3000](https://localhost:3000)
- In the Chrome window that just launched, navigate to your VSTS account where the extension should display
- Your breakpoints will be hit!

# Releasing
When you are ready to release your extension to the public, it's time to create a releaseable package. This will include all the files required for your extension to run.
VSTS will host these files for you.
- (Optionally) Set `public` to `true` in `configs/release.json`. If you leave it on `false`, your extension will only be available to VSTS accounts that you explicitly shared it with.
- Run `npm run package:release`
- A `.vsix` file will be created in the `.\dist\` directory
- Upload this file to the VSTS marketplace and optionally share it with a number of accounts
- Your extension is now live!