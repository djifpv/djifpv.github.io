### [Betaflight](https://github.com/betaflight/betaflight-configurator)从源码构建AndroidApk
[vultr](http://vultr.com) 上买个外网机器(IP韩国,网速快,预装Docker)构建, 内存记得开大点. 用完记得把机器删了要不扣钱.

环境: Linux + Docker
```bash
docker run --rm --user root -w /app -v $PWD/data/app:/app -v $PWD/data/root:/root -it androidsdk/android-28 bash

# 进入docker容器后

git clone --depth=1 https://github.com/nvm-sh/nvm ~/.nvm # 下载nvm, 只用装一次
git clone --depth=1 https://github.com/betaflight/betaflight-configurator # 下载betaflight-configurator源码, 只用下一次

. ~/.nvm/nvm.sh # 启用nvm
nvm install && nvm use && npm i -g yarn # 安装依赖

# gradle 配置
apt install -y gradle
mkdir -p ~/.gradle && printf 'org.gradle.jvmargs=-Xmx2024m -XX:MaxPermSize=512m\norg.gradle.daemon=false'  > ~/.gradle/gradle.properties

cd betaflight-configurator
yarn # 安装npm包

# 生成证书, 密码填password (因为源码里就是password), 有现成的证书也可以
keytool -genkey -alias betaflight -keyalg RSA -validity 36500 -keystore cordova/bundle.keystore

cd cordova
cp build_template.json build.json
sed -i "s/\[INJECTED_BY_GULPFILE\]/password/g" build.json
cd -

yarn gulp release --android # 构建
```

编译生成AAB文件和生成的证书, 下载回本地
自己构建成功的AAB文件和证书:
* [betaflight-configurator_10.8.0_android.aab](../assets/betaflight-configurator_10.8.0_android.aab)
* [bundle.keystore](../assets/bundle.keystore)

用[bundletool](https://github.com/google/bundletool)转换成apk文件即可安装. 这里需要使用上一步生成的证书.
```bash
curl -LO https://github.com/google/bundletool/releases/download/1.10.0/bundletool-all-1.10.0.jar
java -jar bundletool-all-1.10.0.jar build-apks --bundle=betaflight-configurator_10.8.0_android.aab --output=betaflight-configurator_10.8.0_android.apks --ks=bundle.keystore --ks-pass=pass:password --ks-key-alias=betaflight --key-pass=pass:password
mkdir betaflight
tar xvf betaflight-configurator_10.8.0_android.apks -C betaflight
```
apk生成在betaflight文件夹中