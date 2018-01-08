---
layout: post
title:  "macvim youcompleteme on mac"
date:   2018-01-05 16:03:06 +0800
categories: python dlib
---
非可執行之紀錄．

環境:
{% highlight shell %}
Mac      : macOS High Sierra Version 10.13.2
Homebrew : 1.4.2
gcc      : Apple LLVM version 9.0.0 (clang-900.0.39.2)
Boost    : 1.66.0
{% endhighlight %}

Clone:
{% highlight shell %}
git clone YouCompleteMe
cd bundle/YouCompleteMe
git submodule update --init --recursive
{% endhighlight %}

macvim:
{% highlight shell %}
brew install macvim --with-override-system-vim
brew link macvim

brew remove macvim
brew cleanup
{% endhighlight %}

vim:
{% highlight shell %}
vim --version
:python3 print(ycm_state._server_popen.stderr.read())
:messages
{% endhighlight %}

記錄除錯過程，非常混亂．
Xcode:
Xcode from app store 要登入認證才能使用

xcode-select -p
sudo xcode-select -s /Applications/Xcode.app/Contents/Developer
sudo xcodebuild -license accept

重新編譯:
{% highlight shell %}
xz -d clang+llvm-5.0.1-x86_64-apple-darwin.tar.xz
tar xf clang+llvm-5.0.1-x86_64-apple-darwin.tar
mv clang+llvm-5.0.1-final-x86_64-apple-darwin ycm_temp
cd ycm_temp
mkdir llvm_root_dir
mv bin include lib libexec share llvm_root_dir
cd ../ycm_build
make -G "Unix Makefiles" -DPATH_TO_LLVM_ROOT=~/ycm_temp/llvm_root_dir
. ~/.vim/bundle/YouCompleteMe/third_party/ycmd/cpp
cmake --build . --target ycm_core --config Release
{% endhighlight %}
