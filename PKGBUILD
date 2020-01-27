# Maintainer: Albert Graef <aggraef@gmail.com>
# Contributor: Ray Rashif <schiv@archlinux.org>
# Contributor: rtfreedman  (rob<d0t>til<d0t>freedman<aT>googlemail<d0t>com
# Contributor: Marian Laschober <marian.laschober@gmail.com>

pkgname=steinberg-vst36
pkgver=3.6.14
pkgrel=1
pkgdesc="Steinberg's VST SDK (version 3.6)"
arch=('any')
url="http://www.steinberg.net/en/company/developers.html"
license=('custom')
provides=('steinberg-vst')
source=(http://www.steinberg.net/sdk_downloads/vst-sdk_3.6.14_build-24_2019-11-29.zip)
md5sums=('31e635c7ec5250a86bf076a95eefd7fc')
depends=('cmake>=3.4.3'
         'gcc-libs')
optdepends=('libx11: VSTGUI'
            'xorgproto: VSTGUI'
            'libxcb: VSTGUI'
            'xcb-util: VSTGUI'
            'xcb-util-keysyms: VSTGUI'
            'xcb-util-cursor: VSTGUI'
            'libxkbcommon: VSTGUI'
            'libxkbcommon-x11: VSTGUI'
            'fontconfig: VSTGUI'
            'cairo: VSTGUI'
            'sqlite>=3.0.0: VSTGUI'
            'gtkmm3: VSTGUI (editorhost example)'
            'jack2: Jack Audio support (audiohost example)'
	    'ruby: VSTGUI (unittest lcov support)'
            )

package() {
  # copy_vst2_to_vst3_sdk.sh -> add VST 2.x wrapper to 3.x SDK (recommended)
  cd "$srcdir/VST_SDK/"
  cp -r VST2_SDK/public.sdk/source/* VST3_SDK/public.sdk/source

  # install SDK
  cd "$srcdir/"
  mkdir -p "$pkgdir/opt/vst36"
  cp -r VST_SDK/* "$pkgdir/opt/vst36/"

  # install headers
  cd "$srcdir/VST_SDK/VST3_SDK/"
  mkdir -p "$pkgdir/usr/include/vst36/pluginterfaces/vst2.x"
  install -m664 public.sdk/source/vst2.x/* \
    "$pkgdir/usr/include/vst36/pluginterfaces/vst2.x/"
  mkdir -p "$pkgdir/usr/include/vst36/pluginterfaces/vst"
  install -m664 pluginterfaces/vst/* \
    "$pkgdir/usr/include/vst36/pluginterfaces/vst/"

  # install license
  cd "$srcdir/VST_SDK/VST3_SDK/"
  mkdir -p "$pkgdir/usr/share/licenses/$pkgname"
  install -m664 doc/LICENSE.txt "$pkgdir/usr/share/licenses/$pkgname/"
}

# set permissions
# TBD
# chmod 777 /opt/vst36/VST3_SDK/vstgui4/vstgui/uidescription/editing/
# chmod 777 /opt/vst36/my_plugins/

# build example:
#mkdir ~/build
#cmake /opt/vst36/VST3_SDK/
#cmake --build . --target again
#cmake --build . --target validator
#./bin/Debug/validator VST3/Debug/again.vst3
