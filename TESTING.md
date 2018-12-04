# Manual-testing scenarios

- Basic editing experience:
  - Create a snippet, both "new" and from a sample
  - Deletes/renames/etc should work correctly and persist even if you close/re-open the app.
  - When deleting last snippet, editor experience should feel like it's doing "the right thing" (which currently is just creating a new blank snippet; we can consider later popping up the samples/new gallery instead, if we get feedback on this).
- Login to github
  - Should be able to log in
  - Should see your snippets in snippets list
    - Note: This is currently broken on IE (WAC), and somewhat broken on EDGE (WAC). An error appears saying "The security settings in your browser prevent us from creating a dialog box..."
    - Note: Separately, there's an issue with IE on both WAC and Win32 that does not allow for consenting to GitHub OAuth apps via IE. The current workaround is to load [this](https://script-lab-react-beta.azurewebsites.net/) url in Chrome and sign-in and consent in that window. After consenting in Chrome, you should be able to use the GitHub functionality in Win32.
- Import someone elses' snippet
  - From YAML
  - From Gist
  - Both regular and custom functions
  - On import failure, should see error.
  - If import a gist that is already present in the workspace, the user should be prompted to choose whether to open the previously imported gist, import the gist anew, or cancel.
    - Note: today, will only prompt for _your_ gists in the the "my gists" list, but NOT for URLs imported in the Import tab. Bug [#274](https://github.com/OfficeDev/script-lab-react/issues/274) tracks improving this soon.
- Sharing:
  - Copying to clipboard works
  - Can share as gist, public and private
    - Gist URL should be updated in snippet information
  - Can update existing gist
  - Update option should not appear in share menu after importing a gist that you do not own
  - Update option appears in share menu after initial publish of a new gist or a gist that you did not previously own
  - Deleting a gist (on the github website) and then trying to update it from Script Lab should have a reasonable behavior (some sort of error message?)
- Misc:
  - On both editor and runner, should be able to trigger a runtime error via the browser (e.g., type the following into the console: `setTimeout(function() { throw new Error("Test") } , 500)`), and it should trigger an error experience.

By the end of Nov 2018, should also be able to test the following (can skip for now, since we're currently re-using the Script Lab 2017 runner experience):

- Run snippet, in both in-editor runner (the only option for Office 2016 RTM and earlier) and via the "Run" button (run.html), testing that:
  - Snippet renders correctly
  - "Run" from editor or run gallery, in-place refresh, and full refresh all work correctly (render the snippet, don't double-refresh, etc.). The run (either type) doesn't show a "snippet needs reloading" message if the snippet is already fresh.
  - Console log renders correctly (and scrolls correctly, if many lines)
  - Thrown errors from user code are reflected in the console.
  - Erroneous code (e.g, syntax error) shows error correctly.
  - Running deleted snippet has reasonable behavior.
  - [Side-by-side runner]:
    - Edit to code causes runner want to refresh.
    - Whether starting from error or going to error state and back out, should act correctly.
- Ribbon buttons (Add-in):
  - The Script Lab tab is visible with its buttons
  - The buttons aside from Run/Code/Functions open web pages (and this works on all platforms)