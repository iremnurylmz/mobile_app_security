# Mobil Uygulama Güvenliği Araçları İçin Kurulum Rehberi

Bu rehber, mobil uygulama güvenliği testleri için gerekli temel araçların neler olduğunu, nereden indirileceğini ve nasıl kurulacağını açıklar. Amacım, test ortamınızı hızlı ve kolay bir şekilde kurmanıza yardımcı olmaktır.

## İçindekiler
- [Gereksinimler](#gereksinimler)
- [Araçlar](#araçlar)
  - [Genymotion](#genymotion)
  - [ADB](#adb)
  - [Burp Suite](#burp-suite)
  - [Frida Server](#frida-server)
  - [Jadx GUI](#jadx-gui)
  - [MobSF](#mobsf)
  - [Ghidra](#ghidra)
    
## Gereksinimler

Aşağıdaki araçları kullanabilmek için temel bazı gereksinimler bulunmaktadır:

- **Python 3.x** (Frida için gerekli)
  - İndirme linki: [Python İndir](https://www.python.org/downloads/)
  
- **Java 11 veya üzeri** (Jadx, MobSF ve Ghidra için gerekli)
  - İndirme linki: [Java JDK İndir](https://www.oracle.com/java/technologies/downloads/)
  
- **Docker** (MobSF için gerekli)
  - İndirme linki: [Docker İndir](https://docs.docker.com/desktop/install/windows-install/)

    
## Araçlar

## Genymotion

- **Nedir?**  
 Genymotion, Android uygulamalarını sanal cihazlarda test etmek için kullanılan bir Android emülatörüdür. Gerçek cihazlara ihtiyaç duymadan, geniş bir cihaz çeşitliliği sunarak farklı modellerde ve sürümlerde test yapma imkanı sağlar.
  
### Kurulum Adımları:

### 1. Genymotion İndir ve Kur
   - [Genymotion İndir](https://www.genymotion.com/product-desktop/download/)
   - Genymotion sanallaştırma altyapısı olarak VirtualBox kullandığı için **Genymotion Desktop + VirtualBox** olanı indirmelisiniz.
   - İndirilen dosyayı çalıştırın ve kurulum talimatlarını izleyin.

### 2. Genymotion Hesabı Oluştur
   - Genymotion'u kullanabilmek için bir Genymotion hesabına ihtiyacınız olacak. [Kayıt Olun](https://www.genymotion.com/account/create/).
   - Hesap oluşturduktan sonra, Genymotion’u başlatırken giriş yapmanız istenecektir.

### 3. Sanal Cihaz Oluşturma
   - Genymotion’u başlattıktan sonra, cihaz listesine tıklayarak yeni bir sanal cihaz oluşturun.
   - Kullanmak istediğiniz Android sürümünü ve cihaz modelini seçin.
   - Sanal cihazı indirip başlatın.

### 4. VirtualBox Sorun Giderme (Gerekirse)
   - Eğer sanal cihaz başlatma sırasında VirtualBox ile ilgili hatalar alırsanız, VirtualBox'ın doğru sürümünü kurduğunuzdan emin olun ve gerekli ayarları tekrar gözden geçirin.

Bu adımları takip ederek Genymotion'u kolayca kurup Android uygulamalarınızı test edebilirsiniz.

---

## ADB (Android Debug Bridge)

- **Nedir?**
  
  Android Debug Bridge (ADB), Android cihazlar ile bilgisayar arasında iletişim kurmayı sağlayan bir komut satırı aracıdır. ADB ile uygulama yükleme, hata ayıklama, ekran görüntüsü alma, video kaydı yapma ve dosya aktarımı gibi işlemleri kolayca gerçekleştirilebilirsiniz.

- **İndir**: [ADB İndir](https://developer.android.com/tools/releases/platform-tools)

### Kurulum Adımları

ADB'yi kullanmaya başlamak için şu adımları izleyin:

1. **ADB aracını indirin** ve zip dosyasını çıkartın.
2. **ADB dizinini PATH ortam değişkenine ekleyin**. Bunun için şu adımları izleyin: 
    - Başlat Menüsü'nde **"Ortam Değişkenlerini Düzenle"** yazın ve çıkan sonuca tıklayın.
    - Açılan pencerede **Sistem Özellikleri** penceresinde, alt kısımda **Ortam Değişkenleri** butonuna tıklayın.
    - **Kullanıcı Değişkenleri** kısmında **Path**'i bulun ve **Düzenle** butonuna tıklayın.
    - **Yeni** butonuna basarak ADB'nin bulunduğu dizini ekleyin. Örnek dizin:
        ```bash
        C:\Users\Test\Masaüstü\platform-tools
        ```
    - Değişiklikleri kaydetmek için **Tamam** butonuna tıklayın.<br>
    
3. ADB'nin çalıştığını doğrulamak için terminalde şu komutu çalıştırın:
   
    ```bash
    adb version
    ```
    ADB versiyon bilgisi görüntülenirse kurulum başarılı olmuştur.

### Temel Komutlar

- **Bağlı cihazları listele:**
  ```bash
  adb devices
    ```
    Bağlı Android cihazları listeler.

  - **Uygulama yükle:**  
    ```bash
    adb install <apk_dosya_yolu>
    ```
    Cihaza APK yükler.

  - **Dosya aktarımı:**  
    - Bilgisayardan cihaza dosya aktarmak için:
      ```bash
      adb push <yerel_dosya_yolu> <cihaz_dizini>
      ```
      Bilgisayarınızdaki bir dosyayı Android cihazınızdaki belirli bir dizine kopyalar.
    
    - Cihazdan bilgisayara dosya aktarmak için:
      ```bash
      adb pull <cihaz_dosya_yolu> <yerel_dizin>
      ```
      Android cihazınızdaki bir dosyayı bilgisayarınıza çeker.

- **Yardımcı Kaynaklar**:<br>

  Daha fazla bilgi için [ADB](https://developer.android.com/studio/command-line/adb) bağlantısını inceleyebilirsiniz.


---
## Burp Suite

- **Nedir?**   
  Burp Suite, web ve mobil uygulama güvenlik testlerinde kullanılan bir proxy ve analiz aracıdır. Bu araç ile ağ trafiğini yakalayabilir, analiz edebilir ve manipüle edebilirsiniz.

- **İndir**: [Burp Suite İndir](https://portswigger.net/burp/releases/professional-community-2024-7-5?requestededition=community&requestedplatform=)

### Kurulum Adımları

### 1. Proxy Ayarları 
   Burp Suite'in **Proxy** aracını kullanarak trafiği yakalayabiliriz. Proxy ayarlarını yapmak için:
   - **Proxy > Proxy Settings > Proxy Listeners** alanına gidin.
   - Dinlemek istediğiniz portu ayarlayın. Varsayılan olarak port 8080 kullanılır. İstediğiniz portu yazın. Ekran görüntüsü için [tıklayın](https://github.com/user-attachments/assets/2c1f2f26-9494-4274-ab52-afda65a4476c).

### 2. SSL Sertifikası Yükleme
   SSL trafiğini düzgün bir şekilde analiz edebilmek için Android cihazınızın Burp Suite sertifikasına güvenmesi gerekiyor. Bu nedenle, Burp Suite'ten sertifika üretip Android cihazınıza eklemeniz gerekmektedir.

   **Not:** Çoğu blogda “Import / export CA certificate” diyerek .cer uzantılı bir sertifika üretip bunu Android cihaza yüklemeyi gösteriyor. Ancak, PortSwigger sertifikası import edildiğinde sistem üzerinde sadece kullanıcı seviyesinde bir yükleme gerçekleşir. 
   Bu nedenle, uygulamaların yaptığı istekleri incelemek istediğinizde SSL Connection hatası alabilirsiniz. PortSwigger sertifikasını sistem haklarıyla işletim sisteminize import etmek için şu adımları izleyin:
   

   1. **Sertifikayı İndirme**  
      Burp Suite üzerinden sertifikayı .der formatında indirin. Ekran görüntüsü için [tıklayın](https://github.com/user-attachments/assets/6e9dd1cc-1a27-43a6-9b60-f1fe63c386ed).

   2. **Sertifikayı .pem Formatına Çevirme**
      
      **Not:** Sertifikayı indirdikten sonra, bu sertifikayı OpenSSL kullanarak .pem formatına dönüştürmemiz gerekiyor. Android işletim sistemleri sertifikaları .pem formatında bekler ve OpenSSL tarafından verilen sertifikaların                 `subject_hash_old.0` adıyla olması 
      gerekir. Eğer Windows kullanıyorsanız, indirdiğiniz .der uzantılı sertifikayı öncelikle Linux ortamına taşıyın ve ardından terminalde şu komutları sırayla çalıştırın:

      ```bash
      openssl x509 -inform DER -in cacert.der -out cacert.pem
      ```
      ```bash
      openssl x509 -inform PEM -subject_hash_old -in cacert.pem | head -1
      ```
      ```bash
      mv cacert.pem <hash>.0
      ```
  
Bu işlemler sonucunda 9a5ba575.0 adlı dosyamızı oluşturuyoruz. Şimdi ise bu dosyayı sistemimize atalım. Bunun için de 9a5ba575.0 adlı dosyamızı tekrar windows ortamına attıktan sonra Android sistemimize bağlanmak ve dosyamızı aktarmak için ADB(Android Debug Bridge) ’i kullanacağız. <br>

1. Sertifikayı cihazınıza aktarın:
    ```bash
    adb push <hash>.0 /sdcard/
    ```
2. Cihazınıza bağlanın:
    ```bash
    adb shell
    ```
3. Aşağıdaki omutları kullanarak dosyanızı sistem dosyaları içerisinde bulunan sertifikalar kısmına atın.
    ```bash
    mv /sdcard/<hash>.0 /system/etc/security/cacerts/
     ```
    ```bash
    chmod 644 /system/etc/security/cacerts/<hash>.0
    ```

Kurulup kurulmadığını android sisteminize girerek bakabilirsiniz. Ekran görüntüsü için [tıklayın](https://github.com/user-attachments/assets/12eecdf2-a251-48db-9905-15ac5309073d) Sistem hakları ile başarılı bir şekilde kurulduğunu görebiliriz. <br>

Son olarakta Android cihazımızdan ya da emulatörümüzden trafikleri yönlendirmek istediğimiz bilgisayara doğru proxy ayarlarını girmemiz gerekiyor.<br>

Android cihazınızda Burp Suite proxy ayarlarını yapmak için:

- **Ayarlar > Ağ ve İnternet > Wifi > AndroidWifi** menüsünden Proxy ayarlarını **Manual** olarak değiştirin.
  
- Burp Suite'in kurulu olduğu bilgisayarın yerel IP adresini ve ayarladığınız portu girin. Ekran görüntüsü için [tıklayın](https://github.com/user-attachments/assets/df8d9e7f-6225-4287-9d0e-d53d4864935d).

Google'da herhangi bir arama yaparak SSL trafiğinin Burp Suite üzerinde görünüp görünmediğini test edebilirsiniz. <br>

Kaynak için [tıklayın](https://erenn-uygun.medium.com/android-i%CC%87%C5%9Fletim-sistemlerine-sistem-seviyesinde-port-swigger-sertifikas%C4%B1-kurulumu-11db3a2bc08a)


**NOT:** Her uygulamanın SSL trafiği bu kadar basit bir yöntemle alınamayabilir çünkü uygulama tarafında SSL pinning gibi ek güvenlik önlemleri mevcut olabilir. SSL pinning, uygulama trafiği için ek bir güvenlik katmanı sağlayan bir tekniktir. Bu sayede, uygulama yalnızca belirli sertifikalara güvenerek, proxy araçlarının trafiği kesmesine veya manipüle etmesine izin vermez. Ancak, SSL pinning korumasını aşmak için de bazı bypass yöntemleri mevcuttur. Bu aşamada, özellikle güvenlik araştırmalarında kullanılan güçlü bir araç olan Frida devreye girer.

  ---


## Frida Server

- **Nedir?**  
  Frida, dinamik analiz ve canlı müdahale yapmanıza olanak tanıyan güçlü bir araçtır. Uygulamalar üzerinde JavaScript kodu ekleyerek, bu uygulamaların davranışlarını inceleyebilir ve güvenlik açıklarını tespit edebilirsiniz. Frida, metotları yeniden tanımlamanıza ve bypass etmenize       imkan tanır. Ayrıca, SSL pinning ve root algılama gibi güvenlik önlemlerini aşmanıza yardımcı olur.

- **İndir**:  
  Python kullanarak Frida Tools'u yükleyin:

 ```bash
  pip install frida-tools
 ```

- Frida’yı bilgisayarınıza yükledikten sonra Android cihazınıza uyumlu olan Frida Server'ı yüklemeniz gerekmektedir. Android cihazınıza uygun Frida Server'ı indirmek için cihazınızın mimarisini kontrol edin:

```bash
adb shell getprop ro.product.cpu.abi
```

- Komutun çıktısındaki mimariye göre uygun Frida Server'ı [buradan](https://github.com/frida/frida/releases/tag/16.4.10) indirilebilirsiniz. Ekran görüntüsü için [tıklayın](https://github.com/user-attachments/assets/720031d9-0702-42c9-aea6-f46a466f866f)
- İndirilen Frida Server'ı ADB push komutu ile Android cihazınıza aktarın:

```bash
adb push frida-server-16.4.10-android-x86_64 /data/local/tmp/frida-server
```
- Daha sonra ilgili Frida Server ajanına gerekli yetkiler verin.
  
```bash
adb shell “chmod 755 /data/local/tmp/frida-server”
```
- Ardından Frida Server'ı cihaz üzerinde çalıştırın.
  
```bash
adb shell “/data/local/tmp/frida-server &”
```
- Frida Server aktif edildikten sonra Android cihazınızda çalışan işlemleri görüntüleyebilirsiniz:
  
```bash
frida-ps -Uai
```
Ekran görüntüsü için [tıklayın](https://github.com/user-attachments/assets/d5f2950b-b14e-49f3-8ef5-84f191fe66bc).<br>
Bu şekilde Frida kurulumunu bitirmiş oluyoruz.


---

## Jadx GUI
- **Nedir?**  
  Jadx, Android APK dosyalarını decompile ederek kaynak kodlarına ulaşmanızı sağlayan bir araçtır.<br>
  Kullanıcı dostu bir arayüze sahip olan Jadx-Gui, APK dosyalarını analiz etmek ve içerdikleri kodu incelemek için oldukça faydalıdır.

- **Kurulum**:  
  1.  **İndir**: [Jadx-Gui İndir](https://github.com/skylot/jadx/releases). İndirilen dosya bir `.zip` arşiv dosyası olacaktır.

  2. **Arşivi Çıkartın**  
     İndirilen `.zip` dosyasını uygun bir dizine çıkarın

  3. **Jadx-Gui'yı Çalıştırın**  
     Çıkarılan dizinde `bin` klasörüne gidin ve `jadx-gui` çalıştırılabilir dosyasını başlatın:

     - **Windows**:

       ```bash
       bin\jadx-gui.bat
       ```

     - **macOS ve Linux**:

       ```bash
       ./bin/jadx-gui
       ```

  4. **APK Dosyasını Açın**  
     Jadx-Gui'yı başlattıktan sonra, uygulamanın arayüzünden APK dosyanızı açabilirsiniz. Menüden `File > Open` seçeneğini kullanarak APK dosyanızı seçin ve decompile işlemini başlatın.<br>
     
    Bu şekilde Jadx-Gui'yı kurup kullanmaya başlayabilirsiniz.

---


## MobSF 

- **Nedir?**  
  MobSF (Mobile Security Framework), bir apk dosyasının hem dinamik hem de statik analizini gerçekleştirebilen ücretsiz ve açık kaynaklı bir araçtır.

- **İndir**: [MobSF İndir](https://github.com/MobSF/Mobile-Security-Framework-MobSF)
  
- **Kurulum**:  
   Docker kullanarak MobSF'i hızlı bir şekilde kurabilirsiniz.
  
- [Docker İndir](https://docs.docker.com/desktop/install/windows-install/)

### Kurulum

1. **MobSF Docker imajını çekin:**

   Docker kurduktan sonra powershell ekranına gelip aşağıdaki komutu yazarak imajı indirmeniz gerekiyor.
   
   ```bash
   docker pull opensecurity/mobile-security-framework-mobsf
   ```
   Ekran görüntüsü için [tıklayın](https://github.com/user-attachments/assets/a67454e9-1961-43be-b0d9-b216cb7e0728)
   
3. **MobSF Docker konteynerini çalıştırın:**

   Docker imajını başarıyla indirdikten sonra MobSF'i çalıştırmak için şu komutu kullanın: 
   
   ```
   docker run -it --rm -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest
   ```
   Eğer siz farklı bir portta çalışmasını isterseniz -p'den sonraki değeri değiştirmelisiniz.<br>

4. **Tarayıcınızda MobSF arayüzüne erişin:**
   
   Kurulum işlemi bu kadardı. Konteyner başarılı şekilde başlatıldıktan sonra, tarayıcınızı açın ve aşağıdaki URL'yi ziyaret edin:<br>
   (Eğer siz farklı bir port değeri verdiyseniz `:` dan sonra onu yazmanız gerekiyor.)
   ```
   http://localhost:8000
   ```

   Bu adrese giderek MobSF'in kullanıcı arayüzüne erişebilir ve test etmek istediğiniz uygulamanın **APK** dosyasını MobSF arayüzüne sürükleyip bırakarak analiz etmeye başlayabilirsiniz.
   
    **NOT:** Docker'ı kullanmadan da MobSF'i kurabilirsiniz. Ancak, Docker ile kurulum genellikle daha kolaydır ve birçok yapılandırma sorununu otomatik olarak halleder. 
  

--- 

# Ghidra

- **Nedir?**  
  Ghidra, ABD Ulusal Güvenlik Ajansı (NSA) tarafından geliştirilen ve tersine mühendislik için kullanılan ücretsiz ve açık kaynaklı bir yazılımdır. Ghidra, çeşitli yürütülebilir dosya formatlarını analiz edebilir ve dinamik analiz, statik analiz ve kod inceleme 
  gibi işlemleri destekler.


### Kurulum

1. **Ghidra'yı İndirin**: İndirmek için [buraya](https://github.com/NationalSecurityAgency/ghidra/releases) tıklayın. İndirilen dosya genellikle bir ZIP veya TAR dosyası olacaktır.

2. **Ghidra'yı Çıkarın:**
   İndirilen dosyayı uygun bir yere çıkartın.

3. **Ghidra'yı Başlatın:**
     Ghidra'yı başlatmak için ilgili çalıştırılabilir dosyayı kullanın:

     - **Windows**:

       ```bash
       ghidra_<version>/ghidraRun.bat
       ```

     - **macOS ve Linux**:

       ```bash
       ghidra_<version>/ghidraRun
       ```

  4. **Ghidra Arayüzüne Erişin:**
      
       Ghidra başarılı şekilde başlatıldığında, ana arayüzü açılacaktır. Buradan yeni bir proje oluşturabilir ve analiz yapmak için dosyalarınızı ekleyebilirsiniz.<br>

---

**NOT-1:**

Ghidra ilk kez açıldığında, aşağıdaki gibi bir mesaj görebilirsiniz:
  
  ```bash
      Enter path to JDK home directory (ENTER for dialog):
   ```

Bu adım, Ghidra'nın JDK'yı doğru şekilde bulmasını ve uygulamanın çalışmasını sağlar. Bu yüzden JDK yolunu belirtmelisiniz. <br>
JDK:
    
  - **Windows için:** `C:\Program Files\Java\jdk-<version>` altında bulunur.
      
  - **macOS ve Linux: için:** `/usr/lib/jvm/java-<version>` altında bulunur.

Jdk yolunu girdikten sonra Ghidra gerekli Java sürümünü kullanarak doğru şekilde çalışacaktır.

---

**NOT-2:**

  Eğer java sürümünüzün düşük olduğu yönde uyarı alırsanız daha yüksek bir sürüm yüklemelisiniz. Bunun için,<br>

  Java'nın en son sürümünü [buradan](https://www.oracle.com/java/technologies/downloads/) indirip yükleyin.<br>

  Sonrasında tekrar  ghidrayı çalıştırın (3. adım) ve yeni jdk yolunu belirtin. Bu adımdan sonra Ghidra gerekli Java sürümünü kullanarak doğru şekilde çalışacaktır.






