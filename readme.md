### **1. What is an Android Activity, and how is it used in the Android application lifecycle? Explain Localization with reference to Android Studio.**  
An **Android Activity** is a fundamental component of an Android application that represents a single screen with a user interface (UI). It acts as an entry point for user interaction, handling events, and managing UI elements. Activities follow a **lifecycle** managed by the Android system, consisting of key states:  
- **onCreate()** – Called when the activity is created.  
- **onStart()** – Called when the activity becomes visible.  
- **onResume()** – When the activity is in the foreground and interactive.  
- **onPause()** – When another activity comes into focus.  
- **onStop()** – When the activity is no longer visible.  
- **onDestroy()** – Called when the activity is removed from memory.  

**Localization in Android Studio:**  
Localization refers to adapting an app for different languages and regions. It is implemented using **string resources** in XML files inside the `res/values/` folder. Different language versions are stored in `res/values-<language_code>/strings.xml`. Android automatically selects the appropriate version based on the user's device language settings. Developers can test localization using **Android Studio's Translations Editor**.

---

### **2. Describe the difference between an Activity and a Fragment in Android development.**  
An **Activity** is an independent UI component representing a single screen, while a **Fragment** is a reusable, modular UI component that exists within an Activity. Key differences include:  
1. **Lifecycle**: Activities have their own lifecycle managed by the system, whereas Fragments have their lifecycle tied to the hosting Activity.  
2. **Reusability**: Fragments allow for better modularity, as multiple Fragments can exist in a single Activity. Activities, on the other hand, are independent and cannot be embedded.  
3. **Navigation**: Switching between Activities requires explicit Intents, whereas Fragments use Fragment Transactions to add, replace, or remove them dynamically.  
4. **Performance**: Using Fragments instead of multiple Activities improves performance and memory usage since switching between Activities involves heavy system calls.  
5. **UI Adaptability**: Fragments allow for flexible UI design, especially for tablets, where multiple Fragments can be displayed within the same Activity.  

Developers typically use Fragments in modern Android apps to create flexible and efficient UI designs while minimizing Activity transitions.

---

### **3. What are Services in Android, and how do they run in the background?**  
A **Service** in Android is a background component that performs long-running operations without a UI. It is used for tasks such as playing music, fetching data from a server, or handling background tasks like notifications.  

Types of Android Services:  
1. **Foreground Services**: Run in the background but remain visible to the user via a notification (e.g., music players).  
2. **Background Services**: Perform tasks without user interaction and stop when the job is done (e.g., data syncing).  
3. **Bound Services**: Allows components (like Activities) to bind to the service and communicate with it (e.g., accessing media playback controls).  

A Service is started using `startService()` or `bindService()`. Since Android 8.0 (Oreo), background execution limitations require services to use **WorkManager** or **Foreground Service** with a notification. Services are ideal for operations that must continue even when the user leaves the app.

---

### **4. What are permissions in Android, and how does the permission model work?**  
**Permissions** in Android control access to sensitive system resources like location, contacts, storage, and the internet. They ensure that apps only access necessary features while protecting user privacy.  

### **Android Permission Model:**  
1. **Normal Permissions**: These do not require user approval (e.g., Internet access).  
2. **Dangerous Permissions**: Require explicit user consent (e.g., accessing the camera, contacts, or location).  
3. **Signature Permissions**: Granted automatically if the requesting app is signed with the same certificate as the app defining the permission.  

Since Android 6.0 (API level 23), apps must **request dangerous permissions at runtime** using `requestPermissions()` instead of during installation. The user can grant or deny permissions, and apps must handle denied permissions gracefully.  

Example of requesting runtime permission for location:  
```java
ActivityCompat.requestPermissions(this, new String[]{Manifest.permission.ACCESS_FINE_LOCATION}, REQUEST_CODE);
```  
With evolving Android versions, **scoped storage** and **background location limitations** further enhance security while ensuring a smooth user experience.

---

### **5. What is an Intent in Android, and how is it used to start activities and pass data?**  
An **Intent** is a messaging object that allows components (Activities, Services, Broadcast Receivers) to communicate in Android. It facilitates navigation between Activities and transfers data.  

### **Types of Intents:**  
1. **Explicit Intent**: Used to start a specific component within the same app.  
   ```java
   Intent intent = new Intent(CurrentActivity.this, TargetActivity.class);
   startActivity(intent);
   ```  
2. **Implicit Intent**: Used when the app does not specify a target component, relying on the system to find an appropriate one (e.g., opening a URL in a browser).  
   ```java
   Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse("https://example.com"));
   startActivity(intent);
   ```  

### **Passing Data with Intents:**  
Data can be sent using `putExtra()` and retrieved in the target Activity using `getIntent().getStringExtra()`.  
```java
Intent intent = new Intent(this, SecondActivity.class);
intent.putExtra("username", "JohnDoe");
startActivity(intent);
```  
**Intents** also facilitate **broadcast messaging**, enabling apps to respond to system-wide events like battery status changes or incoming SMS.
