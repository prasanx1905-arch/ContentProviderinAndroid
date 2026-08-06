
# Ex.No:4 Create Your Own Content Providers to get Contacts details.


## AIM:

To create your own content providers to get contacts details using Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min. required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as “ex.no.3″ and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Get contacts details and Display details give in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the text create your own content providers to get contacts details.
Developed by: Prasanna A
Registeration Number : 212223220078
*/
```
mainactivity.java
```
package com.example.contactexpt;

import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

import android.Manifest;
import android.annotation.SuppressLint;
import android.content.ContentResolver;
import android.content.pm.PackageManager;
import android.database.Cursor;
import android.net.Uri;
import android.os.Bundle;
import android.provider.ContactsContract;
import android.util.Log;
import android.view.View;

public class MainActivity extends AppCompatActivity {

    private static final int REQUEST_CONTACTS = 100;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    public void btnGetContacts(View v) {
        getPhoneContacts();
    }

    public void getPhoneContacts() {

        if (ContextCompat.checkSelfPermission(this,
                Manifest.permission.READ_CONTACTS)
                != PackageManager.PERMISSION_GRANTED) {

            ActivityCompat.requestPermissions(this,
                    new String[]{Manifest.permission.READ_CONTACTS},
                    REQUEST_CONTACTS);
            return;
        }

        ContentResolver contentResolver = getContentResolver();
        Uri uri = ContactsContract.CommonDataKinds.Phone.CONTENT_URI;

        Cursor cursor = contentResolver.query(uri,
                null,
                null,
                null,
                null);

        if (cursor == null) {
            return;
        }

        Log.i("CONTACT_PROVIDER",
                "TOTAL # of CONTACTS ::: " + cursor.getCount());

        if (cursor.getCount() > 0) {

            while (cursor.moveToNext()) {

                @SuppressLint("Range")
                String contactName = cursor.getString(
                        cursor.getColumnIndex(
                                ContactsContract.CommonDataKinds.Phone.DISPLAY_NAME));

                @SuppressLint("Range")
                String contactNumber = cursor.getString(
                        cursor.getColumnIndex(
                                ContactsContract.CommonDataKinds.Phone.NUMBER));

                Log.i("CONTACT_PROVIDER_DEMO",
                        "Contact Name ::: " + contactName +
                                " Phone Number ::: " + contactNumber);
            }
        }

        cursor.close();
    }


}
```
activityxml code
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center"
    android:orientation="vertical">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Contact Provider"
        android:textSize="24sp"
        android:textStyle="bold"
        android:layout_marginBottom="20dp"/>

    <Button
        android:id="@+id/btnContacts"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Get Contacts"
        android:onClick="btnGetContacts"/>

</LinearLayout>
```


## OUTPUT
<img width="1907" height="1073" alt="Screenshot 2026-07-27 092549" src="https://github.com/user-attachments/assets/ed2826ab-f45f-47aa-9165-42d7b39256be" />




<img width="1908" height="1077" alt="Screenshot 2026-07-27 092608" src="https://github.com/user-attachments/assets/cbd7b74f-13e5-4a61-b151-c914c1e3cd66" />
<img width="1907" height="1073" alt="Screenshot 2026-07-27 092654" src="https://github.com/user-attachments/assets/0272ee51-0e53-40a3-b529-56d19daf92bc" />




## RESULT
Thus a Simple Android Application create your own content providers to get contacts details using Android Studio is developed and executed successfully.
