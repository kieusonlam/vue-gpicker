Vue Google Picker
===================
Simple vue wrapper for [Google Picker API](https://developers.google.com/picker/docs/) 

Based on [react-google-picker](https://github.com/sdoomz/react-google-picker)

Installation
============
```
npm install vue-gpicker
```

Usage
=====
```
<VueGPicker :clientId="'your-client-id'"
            :developerKey="'your-developer-key'"
            :scope="['https://www.googleapis.com/auth/drive.readonly']"
            :onChange="(data) => console.log('on change:', data)"
            :multiselect="true"
            :navHidden="true"
            :authImmediate="false"
            :mimeTypes="['image/png', 'image/jpeg', 'image/jpg']"
            :viewId="'DOCS'">
   <MyCustomButton />
</VueGPicker>
```

## Authentication token

You might want to get the Oauth token in order to use it later, for example
in order to [download the selected file](https://developers.google.com/drive/v3/web/manage-downloads).
You can do so by using `onAuthenticate`:

```
<VueGPicker :clientId="'your-client-id'"
            :developerKey="'your-developer-key'"
            :scope="['https://www.googleapis.com/auth/drive.readonly']"
            :onChange="(data) => console.log('on change:', data)"
            :onAuthenticate="(token) => console.log('oauth token:', token)"
            :multiselect="true"
            :navHidden="true"
            :authImmediate="false"
            :mimeTypes="['image/png', 'image/jpeg', 'image/jpg']"
            :viewId="'DOCS'">
   <MyCustomButton />
</VueGPicker>
```

## Custom build method
You can override the default build function by passing your custom function which receives two arguments:
- `google`: a reference to the window.google object.
- `access_token`: which you will need to pass to `setOAuthToken` method.
```
<VueGPicker :clientId="CLIENT_ID"
            :developerKey="DEVELOPER_KEY"
            :scope="SCOPE"
            :onChange="(data) => console.log('on change:', data)"
            :multiselect="true"
            :navHidden="true"
            :authImmediate="false"
            :viewId='FOLDERS'
            :createPicker="(google, oauthToken) => {
                const googleViewId = google.picker.ViewId.FOLDERS;
                const docsView = new google.picker.DocsView(googleViewId)
                    .setIncludeFolders(true)
                    .setMimeTypes('application/vnd.google-apps.folder')
                    .setSelectFolderEnabled(true);

                const picker = new window.google.picker.PickerBuilder()
                    .addView(docsView)
                    .setOAuthToken(oauthToken)
                    .setDeveloperKey(DEVELOPER_KEY)
                    .setCallback(()=>{
                        console.log('Custom picker is ready!');
                    });

                picker.build().setVisible(true);
            }"
        >
            <span>Click</span>
            <div className="google"></div>
        </GooglePicker>
```
This example creates a picker which shows folders and you can select folders.


Demo
====
```
npm install
npm start
open http://localhost:8080
```

### [Don't forget to add new origins at console.developers.google.com](https://console.developers.google.com)
