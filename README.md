# Ex.No: 5

# Develop a Simple Application for Proximity Sensor Using Sensor Manager in Android Studio

---

## Developed by:RAKSHITHA P
## Registration Number:212223220083


## AIM

To develop a sensor application for proximity sensor using Sensor Manager in Android Studio.

---

## EQUIPMENTS REQUIRED

- Android Studio (Min. Required: Giraffe)
- Android Mobile Device
- USB Cable

---

## ALGORITHM

### Step 1:

Open Android Studio and then click on **File → New → New Project**.

### Step 2:

Enter the Application name as **ProximitySensor** and click **Next**.

### Step 3:

Select the **Minimum SDK as API 24** and click **Next**.

### Step 4:

Select the **Empty Activity** and click **Next**. Finally, click **Finish**.

### Step 5:

Design the layout in `activity_main.xml`.

### Step 6:

Create a `SensorManager` object and access the **Proximity Sensor** using `Sensor.TYPE_PROXIMITY`.

### Step 7:

Implement `SensorEventListener` to detect changes in the proximity sensor.

### Step 8:

When an object is near the device, display **"Object is NEAR"** and change the background color to red.

### Step 9:

When an object is far from the device, display **"Object is FAR"** and change the background color to green.

### Step 10:

Save and run the application on an Android mobile device.

---

## PROGRAM

### 1. activity_main.xml

```xml
<?xml version="1.0" encoding="utf-8"?>

<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    android:padding="16dp">

    <TextView
        android:id="@+id/tvTitle"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Proximity Sensor"
        android:textSize="28sp"
        android:textStyle="bold"
        android:layout_marginBottom="40dp"/>

    <TextView
        android:id="@+id/tvStatus"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Waiting for sensor data..."
        android:textSize="22sp"
        android:gravity="center"/>

</LinearLayout>
```

---

### 2. MainActivity.java

```java

package com.example.proximitysensorapp;

import android.hardware.Sensor;
import android.hardware.SensorEvent;
import android.hardware.SensorEventListener;
import android.hardware.SensorManager;
import android.os.Bundle;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity
        implements SensorEventListener {

    private SensorManager sensorManager;
    private Sensor proximitySensor;
    private TextView tvStatus;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        tvStatus = findViewById(R.id.tvStatus);

        sensorManager = (SensorManager)
                getSystemService(SENSOR_SERVICE);

        if (sensorManager != null) {
            proximitySensor =
                    sensorManager.getDefaultSensor(
                            Sensor.TYPE_PROXIMITY);
        }

        if (proximitySensor == null) {

            tvStatus.setText(
                    "This device has NO proximity sensor.");

            Toast.makeText(
                    this,
                    "No proximity sensor found",
                    Toast.LENGTH_LONG
            ).show();

        } else {

            tvStatus.setText(
                    "Proximity sensor ready.\n" +
                    "Move your hand near the top of the phone.");
        }
    }

    @Override
    protected void onResume() {
        super.onResume();

        if (proximitySensor != null) {

            sensorManager.registerListener(
                    this,
                    proximitySensor,
                    SensorManager.SENSOR_DELAY_NORMAL
            );
        }
    }

    @Override
    protected void onPause() {
        super.onPause();

        if (sensorManager != null) {
            sensorManager.unregisterListener(this);
        }
    }

    @Override
    public void onSensorChanged(SensorEvent event) {

        if (event.sensor.getType() ==
                Sensor.TYPE_PROXIMITY) {

            float distance = event.values[0];

            float maxRange =
                    proximitySensor.getMaximumRange();

            if (distance < maxRange) {

                tvStatus.setText(
                        "Object is NEAR\n" +
                        "Distance: " + distance + " cm");

                getWindow()
                        .getDecorView()
                        .setBackgroundColor(
                                getResources().getColor(
                                        android.R.color.holo_red_dark
                                )
                        );

            } else {

                tvStatus.setText(
                        "Object is FAR\n" +
                        "Distance: " + distance + " cm");

                getWindow()
                        .getDecorView()
                        .setBackgroundColor(
                                getResources().getColor(
                                        android.R.color.holo_green_dark
                                )
                        );
            }
        }
    }

    @Override
    public void onAccuracyChanged(
            Sensor sensor,
            int accuracy) {
    }
}
```

---

## OUTPUT


### When the Object is Near

When an object or hand is brought close to the proximity sensor:

<img width="720" height="1600" alt="image" src="https://github.com/user-attachments/assets/2a84fdf9-a375-483d-8033-2e115ac187f9" />


```text
Object is NEAR
Distance: 0.0 cm
```

The background changes to **RED**.

### When the Object is Far

When the object or hand is moved away from the proximity sensor:

<img width="720" height="1600" alt="image" src="https://github.com/user-attachments/assets/66e53f66-37cb-47f2-8f21-ae00118f0e7a" />


```text
Object is FAR
Distance: 5.0 cm
```

The background changes to **GREEN**.

---

## WORKING

The application uses the **SensorManager** class to access the proximity sensor available on the Android mobile device.

The `Sensor.TYPE_PROXIMITY` is used to obtain the proximity sensor. The application implements `SensorEventListener` to continuously receive changes from the sensor.

When the sensor detects that an object is close to the device, the application displays **"Object is NEAR"** and changes the background color to red.

When the object is moved away from the device, the application displays **"Object is FAR"** and changes the background color to green.

---

## RESULT

Thus, a simple Android application to display the details of the proximity sensor using Sensor Manager in Android Studio was developed and executed successfully.
