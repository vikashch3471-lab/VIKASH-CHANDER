# AVY – Android Starter (v0.1.0)

यह AVY का शुरुआती Android प्रोजेक्ट है। यह अभी पूर्ण Jarvis-जैसा सिस्टम नहीं है; यह हिंदी वॉइस इनपुट, हिंदी Text-to-Speech और कुछ सुरक्षित Android intents का शुरुआती संस्करण है।

## अभी क्या काम करता है
- हिंदी (hi-IN) में बोलकर कमांड पहचानना (फोन के Speech Recognition सेवा पर निर्भर)
- हिंदी में जवाब बोलना (फोन में Hindi TTS उपलब्ध होना चाहिए)
- Google Search, YouTube, Maps खोलना
- WhatsApp, Chrome और Settings खोलना (यदि ऐप इंस्टॉल हो)
- नंबर के लिए Dialer खोलना; नाम से कॉल के लिए Contact Picker खोलना
- Alarm सेट करने की स्क्रीन खोलना
- ऐप के अंदर अपडेट जाँचने का बटन (रिलीज़ सर्वर कॉन्फ़िगर करने के बाद)
- म्यूजिक ऐप / YouTube Music खोलना

## अभी क्या शामिल नहीं है
- APK पहले से compile नहीं है
- हमेशा background में "Hey AVY" wake-word सुनना
- गाने को हर ऐप में next/previous करना
- सीधे कॉल करना या WhatsApp संदेश अपने-आप भेजना
- पूर्ण AI बातचीत / cloud AI brain / long-term memory
- फोन की सभी सेटिंग्स का नियंत्रण

## Windows पर APK बनाने का तरीका
1. Android Studio इंस्टॉल करें: https://developer.android.com/studio
2. Android Studio खोलें और **Open** चुनकर इस फ़ोल्डर `AVY_Android_Starter` को खोलें।
3. Android Studio के SDK Manager से Android SDK Platform 35 और Build Tools इंस्टॉल करें।
4. Gradle Sync पूरा होने दें।
5. मोबाइल में Developer options और USB debugging चालू करें, USB से कंप्यूटर से जोड़ें।
6. **Build > Build Bundle(s) / APK(s) > Build APK(s)** चुनें।
7. APK सामान्यतः `app/build/outputs/apk/debug/app-debug.apk` में बनेगा।

## पहली बार चलाते समय
- माइक्रोफोन अनुमति दें।
- यदि हिंदी आवाज नहीं आती, Android Settings > Accessibility / Text-to-speech output में Hindi voice data इंस्टॉल करें।
- वॉइस कमांड के लिए इंटरनेट / डिवाइस की speech service की उपलब्धता जरूरी हो सकती है।

## सुरक्षा
कॉल के लिए ऐप सीधे कॉल नहीं करता; यह Android Dialer खोलता है ताकि आप नंबर देखकर खुद कॉल शुरू करें। कोई मैसेज या भुगतान अपने-आप नहीं भेजा जाता।


## AVY के ऐप अपडेट कैसे काम करेंगे
ऐप में **अपडेट जाँचें** बटन जोड़ा गया है। इसे वास्तविक अपडेट देने के लिए डेवलपर को अपनी HTTPS वेबसाइट/सर्वर पर `update.json` और नया APK प्रकाशित करना होगा।

उदाहरण `update.json`:
```json
{
  "versionCode": 2,
  "versionName": "0.2.0",
  "apkUrl": "https://YOUR-DOMAIN.example/releases/avy-0.2.0.apk",
  "notes": "नई सुविधाएँ, बेहतर आवाज़ पहचान और सुधार"
}
```

डेवलपर के कदम:
1. `MainActivity.kt` में `updateManifestUrl` को अपने असली HTTPS `update.json` पते से बदलें।
2. हर रिलीज़ में `app/build.gradle` का `versionCode` बढ़ाएँ और `versionName` अपडेट करें।
3. APK को JSON में दिए `apkUrl` पर रखें और JSON में वही नया `versionCode` लिखें।
4. उसी signing key से हर अपडेट APK साइन करें। अलग key से साइन किया APK मौजूदा ऐप के ऊपर अपडेट नहीं होगा।
5. उपयोगकर्ता ऐप में **अपडेट जाँचें** दबाएगा। नया संस्करण मिलने पर डाउनलोड पेज खुलेगा; Android उपयोगकर्ता से इंस्टॉल की पुष्टि माँगेगा।

**महत्वपूर्ण:** यह शुरुआती सुरक्षित update-check flow है, पूर्ण silent auto-update नहीं। Android सामान्य sideloaded ऐप को बिना उपयोगकर्ता की पुष्टि के चुपचाप अपडेट नहीं करने देता। असली सर्वर URL और signing key अभी सेट नहीं किए गए हैं।
