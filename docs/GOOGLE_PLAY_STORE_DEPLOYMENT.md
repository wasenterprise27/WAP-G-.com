# Google Play Store Deployment Guide

## 📱 Publishing WAP G Mining Deals to Google Play Store

This guide will walk you through the process of building and publishing your React Native app to the Google Play Store.

## Prerequisites

Before you start, you need:

1. **Google Play Developer Account** - Sign up at https://play.google.com/console
   - Registration fee: $25 (one-time)
   - You'll need a Google Account

2. **Java Development Kit (JDK)** - Version 11 or higher
   ```bash
   java -version
   ```

3. **Android SDK** - Installed via Android Studio
   ```bash
   # Check Android SDK location
   echo $ANDROID_HOME
   ```

4. **Node.js & npm** - Already installed from project setup

---

## Step 1: Generate a Keystore File

A keystore file is required to sign your APK for release.

### Generate Keystore

```bash
keytool -genkey -v -keystore wapg-mining-release.keystore \
  -keyalg RSA \
  -keysize 2048 \
  -validity 10000 \
  -alias wapg-mining-key
```

**When prompted, enter:**
- Key store password: (choose a strong password)
- Key password: (same as keystore password)
- First and last name: Your Name
- Organization unit: WAP G Enterprise
- Organization: WAP G
- City: Your City
- State: Your State
- Country code: Your Country Code

**Save the keystore file securely!** You'll need it for future updates.

### Store Credentials in gradle.properties

Create `android/gradle.properties`:

```properties
MYAPP_RELEASE_STORE_FILE=wapg-mining-release.keystore
MYAPP_RELEASE_STORE_PASSWORD=your_keystore_password
MYAPP_RELEASE_KEY_ALIAS=wapg-mining-key
MYAPP_RELEASE_KEY_PASSWORD=your_key_password
```

---

## Step 2: Build Release APK

Navigate to the mobile directory:

```bash
cd mobile
```

### Build the APK

```bash
./android/gradlew bundleRelease
```

This creates an Android App Bundle (.aab) at:
```
mobile/android/app/build/outputs/bundle/release/app-release.aab
```

### Or build APK directly (if you prefer)

```bash
./android/gradlew assembleRelease
```

APK location:
```
mobile/android/app/build/outputs/apk/release/app-release.apk
```

---

## Step 3: Prepare Google Play Store Listing

### Create App Listing

1. Go to https://play.google.com/console
2. Click "Create App"
3. Fill in:
   - **App Name:** WAP G Mining Deals
   - **Default Language:** English
   - **App Type:** Select appropriate category
   - **Category:** Business or Shopping
   - **Content Rating:** Complete the form

### Upload Assets

#### Icon & Screenshots

1. **App Icon** (512x512 PNG, required)
   - Save as `icon.png`

2. **Feature Graphic** (1024x500 PNG)
   - Save as `feature-graphic.png`

3. **Screenshots** (at least 2, max 8)
   - Recommended: 1080x1920 PNG
   - Save as `screenshot-1.png`, `screenshot-2.png`, etc.

4. **Video Preview** (optional but recommended)
   - Upload on Play Store directly

### Fill App Details

**Title:**
```
WAP G Mining Deals
```

**Short Description (80 characters):**
```
Premier mining marketplace for tin & minerals with real-time inventory tracking
```

**Full Description (4000 characters):**
```
WAP G Mining Deals is a comprehensive digital marketplace for buying and selling 
mining products, with a focus on tin and other mineral commodities.

Features:
✓ User registration and secure authentication
✓ Real-time inventory tracking
✓ Buy and sell marketplace
✓ Product catalog with photos
✓ Order management and tracking
✓ Integrated payment system (Stripe, PayPal)
✓ Delivery tracking
✓ Admin dashboard and reports
✓ Mobile-friendly responsive design

Our platform provides a complete ecosystem for miners, traders, and buyers to 
connect and conduct business securely and efficiently.

Support: support@wapgmining.com
```

**Privacy Policy URL:**
```
https://github.com/wasenterprise27/WAP-G-.com/blob/dev/PRIVACY_POLICY.md
```

**Terms of Service URL:**
```
https://github.com/wasenterprise27/WAP-G-.com/blob/dev/TERMS_OF_SERVICE.md
```

---

## Step 4: Content Rating

1. Complete the content rating questionnaire
2. Provide answers about app content
3. System will generate rating (usually takes a few minutes)

---

## Step 5: Upload App Bundle

1. Navigate to **Release > Production** in Play Console
2. Click **Create Release**
3. Upload `app-release.aab` file
4. Review app details:
   - Version number
   - Release notes
   - Rollout percentage (start with 5-10% for testing)

**Release Notes Example:**
```
Version 1.0.0 - Initial Release

🎉 Welcome to WAP G Mining Deals!

New Features:
- Complete marketplace for mining products
- Real-time inventory tracking
- Secure payment integration
- Order management and tracking
- Admin dashboard with analytics
- Joke generator for fun breaks!

Bug Fixes:
- Initial release

Thank you for downloading WAP G Mining Deals!
```

---

## Step 6: Review & Test

Before submitting:

1. **Test Account Setup**
   - Create test account in Play Console
   - Download app on test device
   - Test all major flows:
     - User registration
     - Login
     - Browse marketplace
     - Create order
     - Payment flow

2. **Privacy & Security**
   - Verify SSL/TLS for API calls
   - Check sensitive data handling
   - Ensure GDPR compliance

3. **Content Policy**
   - Verify no prohibited content
   - Check ads compliance (if applicable)
   - Ensure no misleading information

---

## Step 7: Submit for Review

1. Review all app information
2. Accept Play Console Developer Agreement
3. Click **Submit for Review**
4. Review process takes 24-72 hours (usually 24 hours)

---

## Step 8: Monitor & Update

### After Approval

- App appears in Google Play Store
- Share link: `https://play.google.com/store/apps/details?id=com.wapgmining.deals`
- Monitor reviews and ratings
- Track install metrics in Play Console

### Future Updates

To release updates:

```bash
# Increment version code in app.json
cd mobile
./android/gradlew bundleRelease
# Upload new .aab file in Play Console
```

---

## Common Issues & Solutions

### Issue: Build Fails with Java Error
**Solution:** Ensure JDK 11+ is installed
```bash
java -version
export JAVA_HOME=/path/to/jdk
```

### Issue: Keystore Not Found
**Solution:** Ensure gradle.properties path is correct
```bash
ls -la android/gradle.properties
```

### Issue: APK Too Large
**Solution:** Enable ProGuard obfuscation in build.gradle
```gradle
minifyEnabled true
proguardFiles getDefaultProguardFile("proguard-android.txt"), "proguard-rules.pro"
```

### Issue: App Rejected for Policy Violation
**Solution:** 
- Review Play Store policies
- Ensure privacy policy is clear
- Check data collection practices
- Remove any prohibited content

---

## App Store Link

Once approved, your app will be available at:

📱 **Google Play Store:**
```
https://play.google.com/store/apps/details?id=com.wapgmining.deals
```

---

## Security Best Practices

1. ✅ Always use HTTPS for API calls
2. ✅ Never commit keystore files to git
3. ✅ Use environment variables for sensitive data
4. ✅ Implement proper authentication
5. ✅ Encrypt sensitive data
6. ✅ Regular security updates

---

## Support & Resources

- **Google Play Console Docs:** https://developer.android.com/distribute
- **React Native Android Docs:** https://reactnative.dev/docs/signed-apk-android
- **Play Store Policy:** https://play.google.com/about/developer-content-policy/
- **Our Support:** support@wapgmining.com

---

## Checklist Before Submission

- [ ] Keystore file created and backed up
- [ ] gradle.properties configured
- [ ] App icon (512x512) ready
- [ ] Screenshots (1080x1920) ready
- [ ] App description written
- [ ] Privacy policy created
- [ ] Terms of service created
- [ ] Content rating completed
- [ ] APK/Bundle built and tested
- [ ] All features tested on real device
- [ ] Version code incremented
- [ ] Release notes written
- [ ] Google Play Developer account activated

---

**Good luck with your submission! 🚀**

*Last Updated: July 8, 2026*
