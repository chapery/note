# react-native

### 手动安装依赖
```bash
# --skip-install 跳过自动安装依赖
npx react-native init testproject --template react-native-template-typescript --skip-install
cd testproject
yarn install
cd ios
# apple m1 使用 arch -arm64 bundle install
bundle install
# apple m1 使用 arch -arm64 bundle exec pod install
bundle exec pod install
```