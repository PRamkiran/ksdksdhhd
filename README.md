5.AIM:Develop an application that uses a menu with 3 options for dialing a
number, opening a website and to send an SMS. On selecting an option, the
appropriate action should be invoked using intents.
XML CODES:
activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayoutxmlns:android="http://schemas.
android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent"
tools:context=".MainActivity">
<WebView
android:layout_width="match_parent"
android:id="@+id/webpage"
android:layout_height="match_parent">
</WebView>
</androidx.constraintlayout.widget.ConstraintLayout>
menu.xml
19 | P a g e
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
<item
android:title="Contact Us"
android:id="@+id/contactus"/>
<item
android:title="Website"
android:id="@+id/website"/>
<item
android:title="Message"
android:id="@+id/message"/>
</menu>
activity_call.xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayoutxmlns:android="http://schemas.
android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent"
tools:context=".CallActivity">
<EditText
android:id="@+id/edtphnnumber"
20 | P a g e
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:ems="10"
android:hint="Enter Phone Number"
android:inputType="phone"
app:layout_constraintBottom_toBottomOf="parent"
app:layout_constraintEnd_toEndOf="parent"
app:layout_constraintStart_toStartOf="parent"
app:layout_constraintTop_toTopOf="parent" />
<Button
android:id="@+id/btncall"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:layout_marginTop="52dp"
android:backgroundTint="#7C7979"
android:text="Call"
app:layout_constraintBottom_toBottomOf="parent"
app:layout_constraintEnd_toEndOf="parent"
app:layout_constraintHorizontal_bias="0.498"
app:layout_constraintStart_toStartOf="parent"
app:layout_constraintTop_toBottomOf="@+id/edtphnnumber"
app:layout_constraintVertical_bias="0.008" />
</androidx.constraintlayout.widget.ConstraintLayout>
21 | P a g e
activity_message.xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayoutxmlns:android="http://schemas.
android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent"
tools:context=".MessageActivity">
<EditText
android:id="@+id/edtphnnumberformsg"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:layout_marginTop="304dp"
android:ems="10"
android:inputType="phone"
android:hint="Enter Phone Number"
app:layout_constraintEnd_toEndOf="parent"
app:layout_constraintHorizontal_bias="0.497"
app:layout_constraintStart_toStartOf="parent"
app:layout_constraintTop_toTopOf="parent" />
<EditText
android:id="@+id/edtmsg"
android:layout_width="wrap_content"
22 | P a g e
android:layout_height="wrap_content"
android:layout_marginTop="60dp"
android:ems="10"
android:inputType="textPersonName"
android:hint="Enter Message"
app:layout_constraintEnd_toEndOf="parent"
app:layout_constraintHorizontal_bias="0.497"
app:layout_constraintStart_toStartOf="parent"
app:layout_constraintTop_toBottomOf="@+id/edtphnnumberformsg" />
<Button
android:id="@+id/btnsend"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:layout_marginTop="88dp"
android:text="Send"
android:backgroundTint="#8C8888"
app:layout_constraintBottom_toBottomOf="parent"
app:layout_constraintEnd_toEndOf="parent"
app:layout_constraintHorizontal_bias="0.498"
app:layout_constraintStart_toStartOf="parent"
app:layout_constraintTop_toBottomOf="@+id/edtmsg"
app:layout_constraintVertical_bias="0.0" />
</androidx.constraintlayout.widget.ConstraintLayout>
23 | P a g e
JAVA CODE:
MainActivity.java
package com.example.csbs05;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.os.Bundle;
import android.view.Menu;
import android.view.MenuInflater;
import android.view.MenuItem;
import android.webkit.WebView;
import android.webkit.WebViewClient;
public class MainActivity extends AppCompatActivity {
 WebView webpage;
 @Override
 protected void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
 setContentView(R.layout.activity_main);
 }
 @Override
 public booleanonCreateOptionsMenu(Menu menu) {
MenuInflaterinflater =getMenuInflater();
inflater.inflate(R.menu.menu,menu);
 return true;
 }
24 | P a g e
 @Override
 public booleanonOptionsItemSelected(@NonNull MenuItem item) {
 if(item.getItemId() == R.id.contactus) {
 Intent i = new Intent(MainActivity.this,CallActivity.class);
 startActivity(i);
 }
 else if(item.getItemId() == R.id.message) {
 Intent intent = new Intent(MainActivity.this,MessageActivity.class);
 startActivity(intent);
 }
else if(item.getItemId() == R.id.website)
 {
 webpage = findViewById(R.id.webpage);
webpage.loadUrl("https://www.cricbuzz.com/");
webpage.setWebViewClient(new WebViewClient());
 }
 return super.onOptionsItemSelected(item);
 }
 @Override
 public void onBackPressed() {
 if(webpage.canGoBack())
 {
webpage.goBack();
 }
 else
25 | P a g e
 {
super.onBackPressed();
 }
 }
}
CallActivity.java
package com.example.csbs05;
import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
public class CallActivity extends AppCompatActivity {
 Button btncall;
EditText edtphnnumber;
 @Override
 protected void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
 setContentView(R.layout.activity_call);
 btncall = findViewById(R.id.btncall);
 edtphnnumber = findViewById(R.id.edtphnnumber);
26 | P a g e
btncall.setOnClickListener(new View.OnClickListener() {
 @Override
 public void onClick(View v) {
 String phnno = edtphnnumber.getText().toString();
 Intent idial = new Intent(Intent.ACTION_DIAL);
idial.setData(Uri.parse("tel:"+phnno));
 startActivity(idial);
 }
 });
 }
}
MessageActivity.java
package com.example.csbs05;
import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
public class MessageActivity extends AppCompatActivity {
 EditText edtphnnumberformsg;
 EditText edtmsg;
27 | P a g e
 Button btnsend;
 @Override
 protected void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
 setContentView(R.layout.activity_message);
 edtmsg = findViewById(R.id.edtmsg);
 edtphnnumberformsg = findViewById(R.id.edtphnnumberformsg);
 btnsend = findViewById(R.id.btnsend);
btnsend.setOnClickListener(new View.OnClickListener() {
 @Override
 public void onClick(View v) {
 String msg = edtmsg.getText().toString();
 String phnno = edtphnnumberformsg.getText().toString();
 Intent imsg = new Intent(Intent.ACTION_SENDTO);
imsg.setData(Uri.parse("smsto:" + Uri.encode(phnno)));
imsg.putExtra("sms_body", msg);
 startActivity(imsg);
 }
 });
 }
}
