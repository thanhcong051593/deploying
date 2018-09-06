# Build
## Mục tiêu 
  - Biết build app ios
  - Biết build app android
## 1. Hướng dẫn build app android
    B1: Bạn chạy câu lệnh dưới để sinh ra keystore
    $ keytool -genkey -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
    
    B2: Setting up gradle variables
    - Truy cập vào đường dẫn  android/app thấy keystore vừa tạo có tên my-release-key.keystore 
    - sửa file ~/.gradle/gradle.properties theo nộ dung dưới đây
    
    MYAPP_RELEASE_STORE_FILE=my-release-key.keystore
    MYAPP_RELEASE_KEY_ALIAS=my-key-alias
    MYAPP_RELEASE_STORE_PASSWORD=*****
    MYAPP_RELEASE_KEY_PASSWORD=*****
    
    B3:  Adding signing config to your app's gradle config
    -  file android/app/build.gradle thêm nội dung sau
          ...
      android {
          ...
          defaultConfig { ... }
          signingConfigs {
              release {
                  if (project.hasProperty('MYAPP_RELEASE_STORE_FILE')) {
                      storeFile file(MYAPP_RELEASE_STORE_FILE)
                      storePassword MYAPP_RELEASE_STORE_PASSWORD
                      keyAlias MYAPP_RELEASE_KEY_ALIAS
                      keyPassword MYAPP_RELEASE_KEY_PASSWORD
                  }
              }
          }
          buildTypes {
              release {
                  ...
                  signingConfig signingConfigs.release
              }
          }
      }
      ...
      
      B4: sinh ra file apk
      - chạy câu lệnh phía dưới bằng terminal
      
      $ cd android
      $ ./gradlew assembleRelease
      
      B5: Truy cập vào android/app/build/outputs/apk/app-release.apk bạn sẽ thấy file apk vừa build xong
      
      link tham khảo: https://facebook.github.io/react-native/docs/signed-apk-android
      
      
## 2. Build app IOS
      
      B1: cài đặt xcode trên macosx( tải xcode từ appstore)
      
      B2: truy cập vào thư mục gốc của dự án và chạy lệnh sau bằng terminal
      $ react-native link
      
      B3: cấu hình xcode để build 
      
      ![alt text](https://github.com/thanhcong051593/deploying/blob/master/19747941055_6ec9e7e2e5_b.jpg "setting")
      
      B4: để tiến hành build
      chọn Product -> archive
      
      B5: Để tới nơi chưa app ios vừa build 
      chọn window
     
# 3. So sánh build app native với build bằng expo


      
      


