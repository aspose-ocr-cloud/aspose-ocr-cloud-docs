---
title: "Recognize Text in Photos on Android device"
type: docs
url: /recognize-text-in-photos-on-android-device/
weight: 10
---

This article shows how to use Aspose.OCR Cloud in an Android application. We shall use the device camera to capture a photo and use the Aspose API to recognize the text. The user will able be to copy the recognized text and paste it into any other application like an email or a text message. You will need the following:

- [Android Developer Tools (ADT)](http://developer.android.com/tools)
- [Aspose.OCR Cloud](http://cloud.aspose.com/)

Before you start:

1. Download, install and configure ADT on your computer.
1. Create and configure an Android Virtual Device or connect a real Android device with your computer for testing.
1. Set up a complete working and testing environment.
### **Create a project**
1. From the **File** menu, select **New**, then **Android Application Project**.
   The **New Android Application** dialog is displayed.
1. Enter **Application Name**, **Project Name** and **Package Name**. Leave the other settings as default.
1. Click **Next**, **Next**, **Next** and **Next**.
1. Click **Finish**.
### **Application UI**
In **Project Explorer** double click *res/layout/activity_main.xml*. *activity_main.xml* is the UI of our application. Right-click it and select **Change Layout** option. Choose **LinearLayout (Vertical)** from the list and click **OK**. From the **Palette** drag a **Button** and a **TextView** to the white background area. Adjust their width, height and position using mouse as shown in the following screenshot:

![todo:image_alt_text](recognize-text-in-photos-on-android-device_1.png)

We want to access the *TextView* within our code, so we must add some identifier for it. Right-click the newly added *TextView*, click **Edit ID**, Enter *text_results* and click **OK**. Now we can access it using R.id.text_results. Go to **Properties** window and clear the property named **Text**. We want to keep our result view blank. Switch to XML view of *activity_main.xml* and add textIsSelectable attribute to *TextView* element.

**activity_main.xml**

```xml

<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"

  ...>

  <TextView

    android:id="@+id/text_results"

    ...

    android:textIsSelectable="true"

    android:text="" />

  ...

</RelativeLayout>

```

Click the newly added button to select and go to the **Properties** window in the right side. Edit the **Text** property and change its value to *Take Photo*. Updating the property will change the label/caption of the button. Scroll down and find another property **On Click**. Change it's value to *captureImage*. We want to associate a Java method called captureImage with the *click* event of this button. We shall discuss the code of the method later below.
### **Application permissions**
Our application will use some features provided by the system, that is the camera, storage and internet connection. We have to acquire permissions for these resources. Locate the file *AndroidManifest.xml* in **Project Explorer** window and double-click to open it. Add the following code under the <manifest> element.

**AndroidManifest.xml**

```xml

<manifest ...>

  ...

  <uses-feature android:name="android.hardware.camera"

          android:required="true" />

  <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"

          android:maxSdkVersion="18" />

  <uses-permission android:name="android.permission.INTERNET" />

  <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />

  ...

</manifest>

```
### **Implementation**
Our code has four major parts.

1. captureImage Send request to camera to capture photo and save it on external device
1. onActivityResult Receive results from camera when our photo is ready.
1. OcrTask Perform API operation for us
1. displayTextResults Display OCR results

We shall implement each portion of our code step-by-step and explain it. Let's start with captureImage. As we can see in previous section, captureImage is the onClick handler of our *Take Photo* button. So the method signature must follow Android specifications:

**MainActivity.java**

```java

public class MainActivity extends ActionBarActivity {

  // ...

  public void captureImage(View view) {

    // ...

  }

  // ...

}

```

To capture an image using camera we use camera intent MediaStore.ACTION_IMAGE_CAPTURE with MediaStore.EXTRA_OUTPUT as intent extras. When MediaStore.EXTRA_OUTPUT is specified the camera intent will save the captured image at our desired location for us.

We need two more things to handle the request-result process i.e. a request identifier and a temporary file where we shall keep the captured image. Let's update our code accordingly and implement the camera feature.

**MainActivity.java**

```java

public class MainActivity extends ActionBarActivity {

  // ...

  protected static final int REQUEST_IMAGE_CAPTURE = 1;

  File tmpfile;

  public void captureImage(View view) {

    Intent i = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);

    if (i.resolveActivity(getPackageManager()) != null) {

    try {

      tmpfile = File.createTempFile("Photo", ".jpg",

          Environment.getExternalStoragePublicDirectory(Environment.DIRECTORY_PICTURES));

    } catch (IOException x) {

      // We are lost :)

      throw new RuntimeException(x);

    }

    i.putExtra(MediaStore.EXTRA_OUTPUT, Uri.fromFile(tmpfile));

    startActivityForResult(i, REQUEST_IMAGE_CAPTURE);

    }

  }



  // ...

}

```

We don't know when the camera activity will complete and our application will resume its normal operation. So we shall wait and listen to the results in background. Android provides onActivityResult method for this purpose. We shall add it to our MainActivity class as specified in Android documentation.

**MainActivity.java**

```java

public class MainActivity extends ActionBarActivity {

  // ...

  @Override

  protected void onActivityResult(int request, int result, Intent data) {

    if (request == REQUEST_IMAGE_CAPTURE && result == RESULT_OK) {

      if (tmpfile == null) {

        Log.e("onActivityResult", "Photo was not saved. Doing nothing");

        return;

      }

      new OcrTask().execute(tmpfile);

      displayTextResults("Uploading photo and recognizing text. This may take a few seconds.");

    }

  }

  // ...

}

```

Here in onActivityResult we have used REQUEST_IMAGE_CAPTURE and tmpfile from captureImage. We also have used OcrTask and displayTextResults, which are our next topic.

OcrTask is a subclass of AsyncTask, which is Android's standard method of performing short duration asynchronous background tasks. As network operation like REST API calls can be delayed sometimes due to network interruptions, so it is forbidden to perform them in main thread on Android platform. We must use AsyncTask to call Aspose for Cloud APIs. Let us add the class to our program and explain each part in detail.

**MainActivity.java**

```java

public class MainActivity extends ActionBarActivity {

  // ...

  public class OcrTask extends AsyncTask<File, Void, String> {

    String requestUrl;

    String appSID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx";

    String appKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

    @Override

    protected void onPreExecute() {

      super.onPreExecute();

	  // Our implementation goes here...

	}

    @Override

    protected String doInBackground(File... params) {

      // Our implementation goes here...

    }

    @Override

    protected void onPostExecute(String result) {

      super.onPostExecute(result);

      // Our implementation goes here...

    }

  }

}

```

We have three methods here. onPreExecute is called before the asynchronous operation is started. It has no parameters. We perform some initial operation in here and prepare a signed request URL. A signed URL means to make sure that we are authorized to make that API call. We require appSID and appKey for this purpose which can be obtained by signing up for free at <http://cloud.aspose.com/>.

**OcrTask.onPreExecute**

```java

@Override

protected void onPreExecute() {

  super.onPreExecute();

  requestUrl = "https://api.aspose.com/v1.1/ocr/recognize?appSID=" + appSID;

  try {

    Mac mac = Mac.getInstance("HmacSHA1");

    mac.init(new SecretKeySpec(appKey.getBytes(), "HmacSHA1"));

    mac.update(requestUrl.getBytes());

    String signature = Base64.encodeToString(mac.doFinal(), Base64.NO_PADDING);

    requestUrl += "&signature=" + signature;

    Log.i("onPreExecute", "Signed request URL: " + requestUrl);

  } catch (Exception x) {

    throw new RuntimeException(x);

  }

}

```

The doInBackground will do the actual API call. We are using HttpUrlConnection as Http client. We shall upload our captured image file. The returned response is in JSON format and HTTP request method is POST. So we shall setup the connection parameters accordingly.

**OcrTask.doInBackground**

```java

@Override

protected String doInBackground(File... params) {

  File file = params[0];

  HttpURLConnection connection = null;

  try {

    FileInputStream fstream = new FileInputStream(file);

    int fsize = fstream.available();

    connection = (HttpURLConnection) new URL(requestUrl).openConnection();

    connection.setRequestMethod("POST");

    connection.setDoOutput(true);

    connection.setRequestProperty("Accept", "application/json");

    connection.setRequestProperty("Content-Length", String.valueOf(fsize));

    OutputStream upload = connection.getOutputStream();

    byte[] buffer = new byte[10240];

    int len;

    while ((len = fstream.read(buffer)) != -1) {

      upload.write(buffer, 0, len);

    }

    upload.close();

    fstream.close();

    InputStream i = connection.getInputStream();

    String text = new Scanner(i).useDelimiter("\\A").next();

    i.close();

    //file.delete();

    Log.i("doInBackground", text);

    return text;

  } catch (FileNotFoundException fnfx) {

    InputStream e = connection.getErrorStream();

    String text = new Scanner(e).useDelimiter("\\A").next();

    Log.i("doInBackground", text);

    return text;

  } catch (Exception x) {

    throw new RuntimeException(x);

  }

}

```

After we have retrieved the results from Aspose.OCR Cloud API, we need a little bit manipulation. As the response is JSON, should now read the recognized text and also check for error, if any. We shall do the manipulation in onPostExecute method.

**OcrTask.onPostExecute**

```java

@Override

protected void onPostExecute(String result) {

  super.onPostExecute(result);

  String text = "";

  try {

    JSONObject json = new JSONObject(result);

    if (json.has("Status") && json.getString("Status").equals("OK")) {

      text = json.getString("Text");

    } else if (json.has("Message")) {

      text = "Error: " + json.getString("Message");

    }

  } catch (JSONException x) {

    throw new RuntimeException(x);

  }

  displayTextResults(text);

}

```

Now comes the simplest and yet important part of our application i.e. display the recognized text results. We simply change the text property of TextView that we added to our UI in the beginning. We added the id text_results and also said that we can reference it from code using R.id.text_results. Here we go:

**MainActivity.java**

```java

public class MainActivity extends ActionBarActivity {

  // ...

  public void displayTextResults(String text) {

    TextView t = (TextView) findViewById(R.id.text_results);

    t.setText(text);

  }

  // ...

}

```

Putting all things together, we have captured an image using device camera, saved the image in a temporary file on external storage, used Aspose.OCR Cloud to recognize text in that image, used AsyncTask for REST API, displayed the results on the screen. User can copy the text and paste it in any other application.
### **Download**
Download the complete working project from [Github repository](https://github.com/AsposeSocialMedia/PhotoOCR_for_Android). You will need appSID and appKey to run this application. Sign up at <https://dashboard.aspose.cloud/> for free to get them.
