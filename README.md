# TrailPlan

TrailPlan is a lightweight travel planner web app backed by Google Sheets. It includes:

- multiple trips with destination, dates, budget, status and notes
- itinerary activities with completion tracking
- budget progress and expense logging
- packing checklists with packed/unpacked state
- installable offline-friendly interface
- browser demo mode until a Google Sheet is connected

## Run The App

Serve this folder with a static file server, then open `index.html`. For example:

```powershell
python -m http.server 8080
```

Open `http://localhost:8080`.

## Use Google Sheets As The Database

1. Create a blank Google Sheet.
2. Open **Extensions > Apps Script** from the sheet.
3. Replace the default script with the contents of `apps-script/Code.gs`.
4. Select `setupSheets`, click **Run**, and approve the Google permission prompts.
5. Click **Deploy > New deployment > Web app**.
6. Set **Execute as** to yourself and **Who has access** to anyone with the link.
7. Copy the `/exec` Web App URL.
8. In TrailPlan, open **Google Sheets Setup**, paste the URL, and click **Connect**.

When the Apps Script code is updated later, edit the existing deployment and deploy a new version before testing the connection again.

## Use The App On Another Device

The Google Sheet stores travel data, but it does not automatically publish the TrailPlan screen. The current `file:///D:/DOCUMENTS/.../index.html` address works only on the computer that has those files.

To use another phone, tablet or computer:

1. Put the app files on a shared web host, such as GitHub Pages, Netlify or your own website, or copy the files to that device and open `index.html`.
2. On the new device, open **Google Sheets Setup** and paste the same Apps Script `/exec` URL. The saved connection is browser-specific.
3. Make sure the Apps Script web app is deployed with **Execute as: Me** and **Who has access: Anyone**.
4. On the other device, open the `/exec` URL directly. A working deployment displays a response beginning with `{"ok":true`. If it requests a sign-in or reports access denied, fix the Apps Script deployment access and deploy a new version.

The script automatically creates these sheet tabs:

| Sheet | Purpose |
| --- | --- |
| `Trips` | Destinations, dates, travelers, budget and trip status |
| `Itinerary` | Scheduled activities connected to each trip |
| `Expenses` | Budget transactions connected to each trip |
| `Packing` | Checklist items and packed state |

## Security Note

The Apps Script deployment URL can write to your travel database. Keep it private and share it only with people who should be able to update the plan.
