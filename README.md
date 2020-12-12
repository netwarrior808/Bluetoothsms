# Bluetoothsms
I need help developing an android sms and eventually mms texting application. It would be useful when you are in say a building with weak connection and you just need to message someone. I need help developing my idea. I started making the sms application.

MainActivity.java
package com.example.sms;

import android.Manifest;
import android.content.pm.PackageManager;
import android.os.Bundle;

import com.google.android.material.floatingactionbutton.FloatingActionButton;
import com.google.android.material.snackbar.Snackbar;

import androidx.appcompat.app.AppCompatActivity;
import androidx.appcompat.widget.Toolbar;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

import android.telephony.SmsManager;
import android.view.View;

import android.view.Menu;
import android.view.MenuItem;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import static android.widget.Toast.*;

public class MainActivity extends AppCompatActivity {

    Button button;

    EditText editText, editText2;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        if (ContextCompat.checkSelfPermission(MainActivity.this,
                Manifest.permission.SEND_SMS) != PackageManager.PERMISSION_GRANTED) {
            if (ActivityCompat.shouldShowRequestPermissionRationale(MainActivity.this,
                    Manifest.permission.SEND_SMS)) {
                ActivityCompat.requestPermissions(MainActivity.this,
                        new String[]{Manifest.permission.SEND_SMS}, 1);


             else{
                    ActivityCompat.requestPermissions(MainActivity.this,
                            new String[]{Manifest.permission.SEND_SMS}, 1);

             else{
                        // do nothing
                    }
                }
            }
        }

            button = (Button)   findViewById(R.id.button);

            editText = (EditText)   findViewById(R.id.editText);
            editText2 = (EditText)   findViewById(R.id.editText2);

            buttson.setOnClickListener(new View.OnClickListener(){
                public void onClick(View view){
                    String number = editText.getText().toString();
                    String sms = editText2.getText().toString();

                    try {
                        SmsManager smsManager = SmsManager.getDefault();
                        smsManager.sendTextMessage(number, null, sms, null, null );
                        makeText(MainActivity.this, "SENT", LENGTH_SHORT).show();
                    } catch (Exception e){
                        makeText(MainActivity.this, "FAILED", LENGTH_SHORT).show();
                    }

                }
            });
                }
        };
        @Override
        public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults ){
            super.onRequestPermissionsResult(requestCode, permissions, grantResults);
            switch (requestCode){
                case 1:{
                    if(grantResults.length>0 && grantResults[0] == PackageManager.PERMISSION_GRANTED){
                        if(ContextCompat.checkSelfPermission(MainActivity.this,
                                Manifest.permission.SEND_SMS) == PackageManager.PERMISSION_GRANTED){
                            makeText(this, "Permission granted.", LENGTH_SHORT).show();

                        }
                    } else{
                        makeText(this, "No Permission granted." LENGTH_SHORT).show();
                    }
                    return;
                }
            }
        }

}
------------------------------------------------------------------------------------------
activity_main.xml

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <EditText
        android:id="@+id/editTextPhone"
        android:layout_width="409dp"
        android:layout_height="wrap_content"
        android:ems="10"
        android:hint="@string/text"
        android:inputType="phone"
        tools:layout_editor_absoluteX="1dp"
        tools:layout_editor_absoluteY="102dp" />

    <EditText
        android:id="@+id/editTextTextPersonName"
        android:layout_width="409dp"
        android:layout_height="wrap_content"
        android:ems="10"
        android:inputType="textPersonName"
        android:gravity="left"
        android:text="@string/name"
        tools:layout_editor_absoluteX="1dp"
        tools:layout_editor_absoluteY="16dp"
        tools:ignore="RtlHardcoded" />

    <Button
        android:text="@string/send"
        android:id="@+id/button"
        android:layout_width="409dp"
        android:layout_height="wrap_content"
        tools:layout_editor_absoluteX="1dp"
        tools:layout_editor_absoluteY="181dp" />

</androidx.constraintlayout.widget.ConstraintLayout>
