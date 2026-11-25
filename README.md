## WORKSHOP 01 --- ADDITION OF TWO NUMBERS
## DATE:25-11-2026

## AIM
To develop an Android application using Android Studio that accepts two numbers from the user, computes their sum, and displays the result in a text box.

## ALGORITHM
```
1.Start the application.

2.Display the input fields for the first number and the second number, a button labelled "Calculate Sum", and a result box.

3.When the user taps the button, read the text entered in both input fields.

4.Check whether both fields are filled. If either is empty, show an error message and stop.

5.Convert both input strings into numeric values.

6.Compute the sum: sum = num1 + num2.

7.Check whether the sum is a whole number. If yes, display it without a decimal part. Otherwise, display it with its decimal part.

8.Show the sum in the result box.

9.If the input is not a valid number, show an error message and stop.

10.End the application.
```

## PROGRAM

ACTIVITY MAIN.XML
```
<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/app_background"
    android:fillViewport="true">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        android:padding="20dp">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="24dp"
            android:text="Addition Calculator"
            android:textColor="@color/text_primary"
            android:textSize="26sp"
            android:textStyle="bold" />

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="4dp"
            android:text="Enter two numbers to find their sum"
            android:textColor="@color/text_secondary"
            android:textSize="15sp" />

        <com.google.android.material.card.MaterialCardView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="24dp"
            app:cardBackgroundColor="@color/surface"
            app:cardCornerRadius="20dp"
            app:cardElevation="4dp"
            app:contentPadding="20dp">

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:orientation="vertical">

                <com.google.android.material.textfield.TextInputLayout
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:hint="First number"
                    style="@style/Widget.Material3.TextInputLayout.OutlinedBox">

                    <com.google.android.material.textfield.TextInputEditText
                        android:id="@+id/etNum1"
                        android:layout_width="match_parent"
                        android:layout_height="wrap_content"
                        android:inputType="numberSigned|numberDecimal"
                        android:maxLines="1" />

                </com.google.android.material.textfield.TextInputLayout>

                <com.google.android.material.textfield.TextInputLayout
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:layout_marginTop="12dp"
                    android:hint="Second number"
                    style="@style/Widget.Material3.TextInputLayout.OutlinedBox">

                    <com.google.android.material.textfield.TextInputEditText
                        android:id="@+id/etNum2"
                        android:layout_width="match_parent"
                        android:layout_height="wrap_content"
                        android:inputType="numberSigned|numberDecimal"
                        android:maxLines="1" />

                </com.google.android.material.textfield.TextInputLayout>

                <com.google.android.material.button.MaterialButton
                    android:id="@+id/btnAdd"
                    android:layout_width="match_parent"
                    android:layout_height="56dp"
                    android:layout_marginTop="20dp"
                    android:text="Calculate Sum"
                    android:textSize="16sp"
                    android:textStyle="bold"
                    app:cornerRadius="12dp" />

            </LinearLayout>
        </com.google.android.material.card.MaterialCardView>

        <com.google.android.material.card.MaterialCardView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="20dp"
            app:cardBackgroundColor="@color/result_background"
            app:cardCornerRadius="20dp"
            app:cardElevation="0dp"
            app:contentPadding="24dp">

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:gravity="center_horizontal"
                android:orientation="vertical">

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:letterSpacing="0.1"
                    android:text="RESULT"
                    android:textColor="@color/primary"
                    android:textSize="13sp"
                    android:textStyle="bold" />

                <TextView
                    android:id="@+id/etResult"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_marginTop="8dp"
                    android:text="—"
                    android:textColor="@color/text_primary"
                    android:textSize="40sp"
                    android:textStyle="bold" />

            </LinearLayout>
        </com.google.android.material.card.MaterialCardView>

    </LinearLayout>
</ScrollView>
```
ACTIVITY MAIN.JAVA
```
package com.example.additionapp;

import android.os.Bundle;
import android.widget.TextView;

import androidx.appcompat.app.AppCompatActivity;

import com.google.android.material.button.MaterialButton;
import com.google.android.material.textfield.TextInputEditText;

public class MainActivity extends AppCompatActivity {

    private TextInputEditText etNum1, etNum2;
    private TextView etResult;
    private MaterialButton btnAdd;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        etNum1 = findViewById(R.id.etNum1);
        etNum2 = findViewById(R.id.etNum2);
        etResult = findViewById(R.id.etResult);
        btnAdd = findViewById(R.id.btnAdd);

        btnAdd.setOnClickListener(v -> addNumbers());
    }

    private void addNumbers() {
        String input1 = etNum1.getText().toString().trim();
        String input2 = etNum2.getText().toString().trim();

        etNum1.setError(null);
        etNum2.setError(null);

        boolean valid = true;
        if (input1.isEmpty()) {
            etNum1.setError("Please enter a number");
            valid = false;
        }
        if (input2.isEmpty()) {
            etNum2.setError("Please enter a number");
            valid = false;
        }
        if (!valid) {
            etResult.setText("—");
            return;
        }

        try {
            double num1 = Double.parseDouble(input1);
            double num2 = Double.parseDouble(input2);
            double sum = num1 + num2;

            if (sum == Math.floor(sum)) {
                etResult.setText(String.valueOf((long) sum));
            } else {
                etResult.setText(String.valueOf(sum));
            }

        } catch (NumberFormatException e) {
            etResult.setText("—");
            etNum1.setError("Invalid number");
        }
    }
}
```
## OUTPUT
UI DESIGN PART :
![alt text](<Screenshot (74).png>)

FINAL OUTPUT :
![alt text](<Screenshot (82).png>)

## RESULT
The application runs successfully. When the user enters two numbers and taps Calculate Sum, the sum is displayed in the result box.