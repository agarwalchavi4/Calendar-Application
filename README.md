

    <?xml version="1.0" encoding="utf-8"?>  
    <android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"  
        xmlns:app="http://schemas.android.com/apk/res-auto"  
        xmlns:tools="http://schemas.android.com/tools"  
        android:layout_width="match_parent"  
        android:layout_height="match_parent"  
        tools:context="com.calendar.MainActivity">  
      
        <TextView  
            android:id="@+id/date"  
            android:layout_width="0dp"  
            android:layout_height="51dp"  
            android:text="Date"  
            android:textAlignment="center"  
            android:textSize="45dp"  
            android:visibility="visible"  
            app:layout_constraintBottom_toBottomOf="parent"  
            app:layout_constraintHorizontal_bias="0.0"  
            app:layout_constraintLeft_toLeftOf="parent"  
            app:layout_constraintRight_toRightOf="parent"  
            app:layout_constraintTop_toTopOf="parent"  
            app:layout_constraintVertical_bias="0.219" />  
      
        <Button  
            android:id="@+id/btngocalendar"  
            android:layout_width="266dp"  
            android:layout_height="47dp"  
            android:text="Go to calendar"  
            tools:layout_editor_absoluteX="47dp"  
            tools:layout_editor_absoluteY="8dp" />  
      
    </android.support.constraint.ConstraintLayout>  
    
    
    

    <?xml version="1.0" encoding="utf-8"?>  
    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"  
        android:orientation="vertical" android:layout_width="match_parent"  
        android:layout_height="match_parent">  
      
        <CalendarView  
            android:id="@+id/calendar"  
            android:layout_width="match_parent"  
            android:layout_height="wrap_content" />  
    </LinearLayout>  

    <?xml version="1.0" encoding="utf-8"?>    
    <manifest xmlns:android="http://schemas.android.com/apk/res/android"    
        package="com.calendar">    
        
        <application    
            android:allowBackup="true"    
            android:icon="@mipmap/ic_launcher"    
            android:label="@string/app_name"    
            android:roundIcon="@mipmap/ic_launcher_round"    
            android:supportsRtl="true"    
            android:theme="@style/AppTheme">    
            <activity android:name=".MainActivity">    
                <intent-filter>    
                    <action android:name="android.intent.action.MAIN" />    
        
                    <category android:name="android.intent.category.LAUNCHER" />    
                </intent-filter>    
            </activity>    
            <activity android:name=".CalendarApplication"></activity>    
        </application>    
        
    </manifest>  



    package com.calendar;    
        
    import android.content.Intent;    
    import android.os.Bundle;    
    import android.support.v7.app.AppCompatActivity;    
    import android.view.View;    
    import android.widget.Button;    
    import android.widget.TextView;    
        
    public class MainActivity extends AppCompatActivity {    
        
        private static final String TAG = "MainActivity";    
        
        private TextView thedate;    
        private Button btngocalendar;    
        
        @Override    
        protected void onCreate(Bundle savedInstanceState) {    
            super.onCreate(savedInstanceState);    
            setContentView(R.layout.activity_main);    
            thedate = (TextView) findViewById(R.id.date);    
            btngocalendar = (Button) findViewById(R.id.btngocalendar);    
        
            Intent incoming = getIntent();    
            String date = incoming.getStringExtra("date");    
            thedate.setText(date);    
        
            btngocalendar.setOnClickListener(new View.OnClickListener() {    
                @Override    
                public void onClick(View v) {    
                    Intent intent = new Intent(MainActivity.this,CalendarApplication.class);    
                    startActivity(intent);    
                }    
            });    
        }    
    }   


package com.calendar;    
        
    import android.content.Intent;    
    import android.os.Bundle;    
    import android.support.annotation.Nullable;    
    import android.support.v7.app.AppCompatActivity;    
    import android.util.Log;    
    import android.widget.CalendarView;    
        
    public class CalendarApplication extends AppCompatActivity {    
        
        private  static final String TAG = "CalendarApplication";    
        private CalendarView mCalendarView;    
        @Override    
        protected void onCreate(@Nullable Bundle savedInstanceState) {    
            super.onCreate(savedInstanceState);    
            setContentView(R.layout.calendar_layout);    
            mCalendarView = (CalendarView) findViewById(R.id.calendarView);    
            mCalendarView.setOnDateChangeListener(new CalendarView.OnDateChangeListener() {    
                @Override    
                public void onSelectedDayChange(CalendarView CalendarView, int year, int month, int dayOfMonth) {    
                  String date = year + "/" + month + "/"+ dayOfMonth ;    
                    Log.d(TAG, "onSelectedDayChange: yyyy/mm/dd:" + date);    
                    Intent intent = new Intent(CalendarApplication.this,MainActivity.class);    
                    intent.putExtra("date",date);    
                    startActivity(intent);    
        
                }    
            });    
        }    
    }    


 
