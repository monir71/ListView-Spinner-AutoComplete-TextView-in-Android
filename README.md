MainActivity.java File:

```
package com.example.listviewspinnerautocompletetextview;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_main);

        Intent intent = new Intent(getApplicationContext(), ListActivity.class);

        Button btn = findViewById(R.id.button);
        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                startActivity(intent);
            }
        });

        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {
            Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);
            return insets;
        });
    }
}
```

ListActivity.java File:

```
package com.example.listviewspinnerautocompletetextview;

import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.AutoCompleteTextView;
import android.widget.ListView;
import android.widget.Spinner;
import android.widget.Toast;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;

import java.util.ArrayList;

public class ListActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_list);

        //Working with ListView
        ListView listView = findViewById(R.id.listView);

        ArrayList<String> list = new ArrayList<>();
        list.add("Monir");
        list.add("Taquii");
        list.add("Baby");

        ArrayAdapter<String> adapter = new ArrayAdapter<>(getApplicationContext(), android.R.layout.simple_list_item_1, list);
        listView.setAdapter(adapter);

        listView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                switch (position)
                {
                    case 0:
                        Toast.makeText(ListActivity.this, "Monir", Toast.LENGTH_SHORT).show();
                        break;
                    case 1:
                        Toast.makeText(ListActivity.this, "Baby", Toast.LENGTH_SHORT).show();
                        break;
                    case 2:
                        Toast.makeText(ListActivity.this, "Taquii", Toast.LENGTH_SHORT).show();
                        break;
                }
            }
        });

        //Working with Spinner

        ArrayList<String> spnArrayList = new ArrayList<>();
        spnArrayList.add("Mango");
        spnArrayList.add("Jackfruit");
        spnArrayList.add("Guava");
        spnArrayList.add("Pineapple");
        spnArrayList.add("Berry");
        spnArrayList.add("Banana");
        spnArrayList.add("Apple");
        spnArrayList.add("Orange");

        ArrayAdapter spnAdapter = new ArrayAdapter(getApplicationContext(), android.R.layout.simple_spinner_dropdown_item, spnArrayList);

        Spinner spn = findViewById(R.id.spn);
        spn.setAdapter(spnAdapter);

        //Working with AutoComplete TextView

        ArrayList<String> acArrayList = new ArrayList<String>();
        acArrayList.add("Prime Minister");
        acArrayList.add("Minister");
        acArrayList.add("Deputy Minister");
        acArrayList.add("State Minister");
        acArrayList.add("Secretary");
        acArrayList.add("Joint Secretary");
        acArrayList.add("Deputy Secretary");
        acArrayList.add("Assistant Secretary");

        ArrayAdapter<String> acAdapter = new ArrayAdapter<>(getApplicationContext(), android.R.layout.simple_list_item_1, acArrayList);

        AutoCompleteTextView acTextView = findViewById(R.id.actextview);

        acTextView.setAdapter(acAdapter);




        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {
            Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);
            return insets;
        });
    }
}
```
