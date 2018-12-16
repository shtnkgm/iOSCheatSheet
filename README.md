# iOS CheatSheet
CheetSheet for iOS Developer

## KeyChain

```bash
# print certificates
security find-identity -p codesigning -v
```

## CocoaPods

```bash
# Clear Pods
rm -rf Pods; rm Podfile; rm Podfile.lock 

# Init Pods
pod init
atom Podfile

pod install
pod update

# Create PodSpec
pod spec create pod_name

# Lint PodSpec
pod lib lint

# Create Trunk Account 
pod trunk register mail_address 'your_name'

# Publish Pods
pod trunk push pod_name.podspec

# Delete Caches
pod cache clean --all
```

## Carthage

```bash
carthage bootstrap --platform iOS --cache-builds
carthage update --platform iOS --cache-builds

# Create XCFileList
ls Carthage/Build/iOS | grep -E .+framework$ | sed 's/.*/$(SRCROOT)\/Carthage\/Build\/iOS\/&/' > CarthageInput.xcfilelist

# Build for Check Library
carthage build --no-skip-current 

# Delete Caches
rm -rf ~/Library/Caches/org.carthage.CarthageKit 
rm -rf ~/Library/Caches/carthage
```

## Fastlane

```bash
# Init fastlane
fastlane init
fastlane add_plugin versioning

# Download Metadata
fastlane deliver download_metadata　 --force

# Upload Metadata
fastlane deliver --force --skip_screenshots --skip_binary_upload --skip_app_version_update

# Download Screenshot
fastlane deliver download_screenshots --force

# Create Screenshot
fastlane frameit(path: './fastlane/screenshots/', white: false)

# Upload Screenshot
fastlane deliver --force --skip_binary_upload --skip_metadata --skip_app_version_update --overwrite_screenshots

# Upload Binary
fastlane deliver --force --skip_screenshots --skip_metadata --skip_app_version_update

# Submit for Review
fastlane deliver --force --skip_screenshots --skip_metadata --skip_app_version_update  --skip_binary_upload --automatic_release --submit_for_review

# Delete Cookie
rm ~/.fastlane/spaceship/**/cookie
```

## Create Gif
```bash
ffmpeg -i sample_01.mov -vf scale=400:-1 -r 20 sample_01.gif
```

## Swift Compiler
```bash
# Parse and type-check input file(s) and pretty print AST(s)
swiftc -print-ast file
# Parse and type-check input file(s) and dump AST(s)
swiftc -dump-ast file
```

## SwiftLint

```bash
swiftlint
swiftlint autocorrect
swiftlint generate-docs

# Copy All Opt-In Rules
swiftlint rules | awk -F "|" '$3 ~ "yes" { print $2 }' | tr -d ' ' | sed 's/^/  - /' | pbcopy

# Delete Caches
rm -rf ~/Library/Caches/SwiftLint
```

## Xcode

```
# check number of cores, and set number to build
system_profiler SPHardwareDataType
defaults write com.apple.dt.Xcode IDEBuildOperationMaxNumberOfConcurrentCompileTasks [number_of_core]

# show build time
defaults write com.apple.dt.Xcode ShowBuildOperationDuration YES

# print targets, configurations, schemes
xcodebuild -list

# print sdks
xcodebuild -showsdks

## Clean
rm -rf ~/Library/Caches/com.apple.dt.Xcode/
xcodebuild clean
xcodebuild -alltargets clean
rm -rf ~/Library/Developer/Xcode/DerivedData/
xcrun --kill-cache
xcrun simctl erase all
rm -rf ~/Library/Developer/Xcode/iOS\ DeviceSupport/*/Symbols/System/Library/Caches
rm -rf "$(getconf DARWIN_USER_CACHE_DIR)/org.llvm.clang/ModuleCache"
rm -rf "$(getconf DARWIN_USER_CACHE_DIR)/org.llvm.clang.$(whoami)/ModuleCache"
```

## HomeBrew

```bash
# Delete Caches
rm -rf ~/Library/Caches/Homebrew
brew cleanup -s
rm -rf $(brew --cache)
```

## Git

```bash
# Create .gitignore
gibo dump Swift Xcode >> .gitignore

# Download .gitignore for iOS (https://gist.github.com/shtnkgm/dfe0a0478a15de11ce93ca6f39223cd5)
wget https://bit.ly/shtnkgmgi2 -O .gitignore

# Quick Push .gitignore
git add .gitignore;git commit -m "add .gitignore"

# Quick Push Igonored Files
git rm -r --cached .;git add .;git commit -m "rm ignore files"

# Quick Push Fix
git add .;git commit -m "fix";git push
```

