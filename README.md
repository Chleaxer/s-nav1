package com.example.myapplicat;

import android.os.Bundle;

import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity
{

    @Override
    protected void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);


        EditText editTextMesafe = findViewById(R.id.editTextText_km);                           // Mesafe girişi için EditText
        EditText editTextYakitFiyati = findViewById(R.id.editTextText2_yakıt);                  // Yakıt fiyatı girişi için EditText
        EditText editTextYakitTuketim = findViewById(R.id.editTextText3_litre);                 // Yakıt tüketimi girişi için EditText
        Button buttonHesapla = findViewById(R.id.button_hesapla);                               // Hesaplama butonu
        TextView textViewSonuc = findViewById(R.id.textView3_sonuc);                            // Sonucu göstermek için TextView


        buttonHesapla.setOnClickListener(v ->
        {                                                                                       // Butona tıklandığında çalışır
                                                                                                // Giriş değerlerini string olarak al
            String mesafeStr = editTextMesafe.getText().toString();
            String yakitFiyatiStr = editTextYakitFiyati.getText().toString();
            String yakitTuketimStr = editTextYakitTuketim.getText().toString();


            if (mesafeStr.isEmpty() || yakitFiyatiStr.isEmpty() || yakitTuketimStr.isEmpty())
            {
                textViewSonuc.setText("Lütfen tüm alanları doldurun!");
            } else {

                Double mesafe = parseDoubleSafely(mesafeStr);
                Double yakitFiyati = parseDoubleSafely(yakitFiyatiStr);
                Double yakitTuketim = parseDoubleSafely(yakitTuketimStr);

                if (mesafe == null || yakitFiyati == null || yakitTuketim == null)
                {                                                                                 // Geçersiz sayı kontrolü yapar
                    textViewSonuc.setText("Lütfen geçerli sayılar girin!");                       // Geçersizse hata mesajı göster
                } else
                {
                                                                                                 // Değerlerin negatif olup olmadığını kontrol eder
                    if (mesafe < 0 || yakitFiyati < 0 || yakitTuketim < 0)
                    {
                        textViewSonuc.setText("Lütfen Geçersiz değer girmeyin!");
                    } else
                    {
                                                                                                 // Toplam yakıt tüketimini hesapla (litre cinsinden)
                        double toplamYakitTuketim = (mesafe / 100) * yakitTuketim;               // Mesafeye göre yakıt tüketimi

                                                                                                 // Toplam maliyeti hesapla
                        double toplamMaliyet = toplamYakitTuketim * yakitFiyati;                 // Yakıt tüketimi ve fiyatla maliyet


                        textViewSonuc.setText(String.format("Gidilecek mesafede harcanan yakıt tutarı: %.2f TL", toplamMaliyet)); // Sonucu ekrana yazdır
                    }
                }
            }
        });
    }

                                                                                                 // Stringi Double'a  çeviren yardımcı metod
    private Double parseDoubleSafely(String deger)
    {
        try
        {                                                                                            // Hata kontrolü için try-catch bloğu
            return Double.parseDouble(deger);                                                       // Stringi Double'a çevirir
        }
        catch (NumberFormatException e)
        {                                                                                           // Sayı formatı hatası yakala
            return null;                                                                            // Hata olursa null döndür
        }
    }
}


-----------------------------------------------------------------------

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/textView"
        android:layout_width="183dp"
        android:layout_height="65dp"
        android:text="Bilgiler"
        android:textColor="#4B0ABF"
        android:textSize="45sp"
        tools:layout_editor_absoluteX="36dp"
        tools:layout_editor_absoluteY="27dp" />

    <EditText
        android:id="@+id/editTextText3_litre"
        android:layout_width="334dp"
        android:layout_height="48dp"
        android:ems="10"
        android:hint="Yakıt litre fiyatı"
        android:inputType="text"
        tools:layout_editor_absoluteX="39dp"
        tools:layout_editor_absoluteY="273dp" />

    <EditText
        android:id="@+id/editTextText2_yakıt"
        android:layout_width="334dp"
        android:layout_height="48dp"
        android:ems="10"
        android:hint="100 km deki yakıt tüketim(litre)"
        android:inputType="text"
        tools:layout_editor_absoluteX="39dp"
        tools:layout_editor_absoluteY="207dp" />

    <EditText
        android:id="@+id/editTextText_km"
        android:layout_width="334dp"
        android:layout_height="48dp"
        android:ems="10"
        android:hint="Mesafe(km)"
        android:inputType="text"
        tools:layout_editor_absoluteX="39dp"
        tools:layout_editor_absoluteY="137dp" />

    <Button
        android:id="@+id/button_hesapla"
        android:layout_width="339dp"
        android:layout_height="68dp"
        android:text="Hesapla"
        android:textSize="20sp"
        tools:layout_editor_absoluteX="36dp"
        tools:layout_editor_absoluteY="395dp" />

    <TextView
        android:id="@+id/textView2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Gidilecek mesafede harcanan yakıt tutarını hesaplar"
        tools:layout_editor_absoluteX="38dp"
        tools:layout_editor_absoluteY="356dp" />

    <TextView
        android:id="@+id/textView3_sonuc"
        android:layout_width="334dp"
        android:layout_height="51dp"
        android:text="Gidilecek mesafede harcanan yakıt tutarı"
        android:textSize="16sp"
        tools:layout_editor_absoluteX="38dp"
        tools:layout_editor_absoluteY="493dp" />

</androidx.constraintlayout.widget.ConstraintLayout>


----------------------------------------------------------------

import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;
