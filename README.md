Imei-Bul
========

Android cihazınızın IMEI numarasını kısa yoldan öğrenmenizi sağlar. Telefon üzerinden *#06# tuşlayarakda öğrenilen IMEI numarası benzersiz bir numaradır ve sadece size özeldir.


Android cihazınızın IMEI numarasını kısa yoldan öğrenmenizi sağlar. Telefon üzerinden *#06# tuşlayarakda öğrenilen IMEI numarası benzersiz bir numaradır ve sadece size özeldir.

Soru görüş ve öneri için : http://goo.gl/HThiG


Imei, Imei find, Imei number, Imei ara, Imeı bul

--------------------------
Eclipse ile Android projemizi oluşturduktan sonra "activity_main.xml" dosyamız aşağıdaki gibidir.

<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:background="@drawable/main_bos"
tools:context=".MainActivity" >

<TextView
android:id="@+id/textView1"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:layout_alignParentTop="true"
android:layout_centerHorizontal="true"
android:text="IMEI"
android:textColor="#FFFFFF"
android:textSize="77sp" />

<TextView
android:id="@+id/textView2"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:layout_centerHorizontal="true"
android:layout_centerVertical="true"
android:text="123456789012345"
android:textColor="#FFFFFF"
android:textSize="26sp" />

<ImageButton
android:id="@+id/imageButton1"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:layout_alignParentBottom="true"
android:layout_below="@+id/textView2"
android:layout_centerHorizontal="true"
android:background="@drawable/button_back"
android:src="@drawable/copy" />

</RelativeLayout>



layout dosyamız hazır olduğuna göre sıra java dosyamıza geldi.

"MainActivity.java" dosyamızın içeriği aşağıdadır.

package com.imei.imeibul;

import android.os.Bundle;
import android.annotation.SuppressLint;
import android.app.Activity;
import android.content.ClipData;
import android.telephony.TelephonyManager;
import android.view.Menu;
import android.view.View;
import android.widget.ImageButton;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends Activity {

TextView deviceInfo;
TelephonyManager telephonyManager;

@Override
protected void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.activity_main);

final TextView textview2 = (TextView)findViewById(R.id.textView2);
ImageButton imagebutton1 = (ImageButton)findViewById(R.id.imageButton1);

telephonyManager = ((TelephonyManager)getSystemService("phone"));
textview2.setText(telephonyManager.getDeviceId());

imagebutton1.setOnClickListener(new View.OnClickListener() {
@SuppressLint("NewApi")
@Override
public void onClick(View v) {
int currentapiVersion = android.os.Build.VERSION.SDK_INT;
if (currentapiVersion >= android.os.Build.VERSION_CODES.HONEYCOMB){
android.content.ClipboardManager clipboard = (android.content.ClipboardManager) getSystemService(CLIPBOARD_SERVICE); 
ClipData clip = ClipData.newPlainText("imei", textview2.getText().toString());
clipboard.setPrimaryClip(clip); 
} else{
android.text.ClipboardManager clipboard = (android.text.ClipboardManager)getSystemService(CLIPBOARD_SERVICE); 
clipboard.setText(textview2.getText().toString());
}
Toast.makeText(getApplicationContext(), "Text copied to clipboard", Toast.LENGTH_SHORT).show(); 
}
});//imagebutton1.setOnClickListener
}

@Override
public boolean onCreateOptionsMenu(Menu menu) {
// Inflate the menu; this adds items to the action bar if it is present.
getMenuInflater().inflate(R.menu.activity_main, menu);
return true;
}

}



burada imei' nin bulunduğu satırlar;

telephonyManager = ((TelephonyManager)getSystemService("phone"));
textview2.setText(telephonyManager.getDeviceId());

dır. 



İyi çalışmalar.





