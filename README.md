## [v2rayNG](https://github.com/2dust/v2rayNG) - Building and Testing (Using GitHub Actions)

This repository contains a GitHub Actions workflow that automates the process of building the v2rayNG Android app from the latest source code. The workflow generates a signed APK file, which can be downloaded from the GitHub Releases section of your repository.

**Steps:**

1. **Generate a Signing Certificate:**

   a. Download and install the latest [Java Development Kit (JDK)](https://www.oracle.com/java/technologies/downloads/).

   b. Open a terminal in the `bin` folder of the JDK installation directory.

   c. Generate a signing certificate using the following command, replacing the placeholders with your desired values:

   ```
   keytool -genkey -v -keystore keystore.jks -alias <YOUR_ALIAS> -storepass <STORE_PASSWORD> -keypass <KEY_PASSWORD> -validity 365 -keyalg RSA -keysize 2048
   ```

   **Important:** Replace `<YOUR_ALIAS>`, `<STORE_PASSWORD>`, and `<KEY_PASSWORD>` with unique values you'll remember.

   d. Encode the `keystore.jks` file to base64:

   ```
   openssl base64 < keystore.jks | tr -d '\n' > keystore_base64.txt
   ```

2. **Configure GitHub Actions Secrets:**

   a. [fork this repo](https://github.com/oXIIIo/v2rayNG/fork)

   b. In your forked repository, navigate to **Settings** -> **Secrets and Variables** -> **Actions** -> **New repository secret**.

   c. Add the following secrets, replacing the placeholders with your chosen values:

   | Secret Name | Description |
   |---|---|
   | `SIGNING_KEY` | The base64 encoded content of `keystore_base64.txt` |
   | `SIGNING_KEY_ALIAS` | The alias you used when generating the certificate (e.g., `<YOUR_ALIAS>`) |
   | `SIGNING_KEY_PASSWORD` | The password you used for the key (e.g., `<KEY_PASSWORD>`) |
   | `SIGNING_STORE_PASSWORD` | The password you used for the keystore (e.g., `<STORE_PASSWORD>`) |

3. **Trigger the Build Workflow:**

   a. Navigate to the **Actions** tab in your repository.

   b. Select the workflow named "Build v2rayNG APK".

   c. Click the **Run workflow** button.

   d. Optionally, provide values for the following workflow inputs:

      * `XRAY_CORE_VERSION`: Specify the commit hash or short hash for Xray-core (defaults to `HEAD~0`).
      * `V2RAYNG_VERSION`: Set the desired version for v2rayNG (not critical).

4. **Download the Built APK:**

   Once the workflow finishes successfully, the built APK will be uploaded to the **Releases** section of your repository. You can download it from there for installation on your Android device.


By following these steps, you can easily build and test the latest version of the v2rayNG app with the latest Xray-core code and Go version.

# Buy me a coffee ☕
If you find this project helpful, you can buy me a coffee using the donation button below:

<a href="https://nowpayments.io/donation?api_key=MG750CX-D7AMMH9-QWARQ7V-9ZKH9XQ&source=lk_donation&medium=referral" target="_blank">
  <img src="https://nowpayments.io/images/embeds/donation-button-black.svg" alt="Crypto donation button by NOWPayments">
</a>
