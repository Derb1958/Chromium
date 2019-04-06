# Maintainer: Gustavo Alvarez <sl1pkn07@gmail.com>
# Contributor: Mikhail Vorozhtsov <mikhail.vorozhtsov@gmail.com>
# Contributor: Nagisa <simonas@kazlauskas.me>
# Contributor: Misc <andreas.reis@gmail.com>
# Contributor: Jeagoss <jgoliver@jeago.com>
# Contributor: Saikrishna Arcot <saiarcot895@gmail.com> and Steven Newbury <steve@snewbury.org.uk> (First Authors of VAAPI patch)

#########################
## -- Build options -- ##
#########################

_use_wayland=0           # Build Wayland NOTE: extremely experimental and don't work at this moment

##############################################
## -- Package and components information -- ##
##############################################
pkgname=chromium-dev
pkgver=75.0.3753.4
pkgrel=1
pkgdesc="The open-source project behind Google Chrome (Dev Channel)"
arch=('x86_64')
url='http://www.chromium.org'
license=('BSD')
depends=(
#          'libsrtp'
         'libxslt'
         'libxss'
         'minizip'
         'nss'
         'pciutils'
         're2'
         'snappy'
         'xdg-utils'
#          'protobuf'
#          'libevent'
#          'ffmpeg'
#          'icu'    # https://crbug.com/678661.
         'gtk3'
         'openh264'
         'vulkan-icd-loader'
         'libpulse'
#          'libwebp'
         'opus'
         'libva'
         )
makedepends=(
             'gperf'
             'ninja'
             'python2-protobuf'
             'python2-beautifulsoup4'
             'python2-html5lib'
             'python2-simplejson'
             'python'
             'yasm'
             'git'
             'hwids'
             'nodejs'
             'gn-git'
             )
optdepends=(
            'pepper-flash: PPAPI Flash Player'
            'chromium-widevine-dev: Widevine plugin (eg: Netflix) (Dev Channel)'
            #
            'kdialog: Needed for file dialogs in KF5'
            'kwalletmanager: Needed for storing passwords in KWallet5'
            #
            'ttf-font: For some typography'
            #
            'libappindicator-gtk3: Needed for show systray icon in the panel on GTK3 Desktop based'
            #
            'libva-vdpau-driver-chromium: HW video acceleration for NVIDIA users'
            'libva-mesa-driver: HW video acceleration for Nouveau, R600 and RadeonSI users'
            'libva-intel-driver: HW video acceleration for Intel G45 and HD users'
            )
source=(
        #"https://gsdview.appspot.com/chromium-browser-official/chromium-${pkgver}.tar.xz"
        "https://commondatastorage.googleapis.com/chromium-browser-official/chromium-${pkgver}.tar.xz"
        'git+https://github.com/foutrelis/chromium-launcher.git'
        'chromium-dev.svg'
        # Patch form Gentoo.
        # Misc Patches.
        'enable-vaapi.patch' # Use Saikrishna Arcot patch again :https://raw.githubusercontent.com/saiarcot895/chromium-ubuntu-build/4d40b58013b518373b2544d486d3de40796edd36/debian/patches/enable_vaapi_on_linux_2.diff'
        'chromium-ffmpeg-clang.patch'
        # Patch from crbug (chromium bugtracker) or Arch chromium package.
        'chromium-widevine-r4.patch::https://git.archlinux.org/svntogit/packages.git/plain/trunk/chromium-widevine.patch?h=packages/chromium'
        'chromium-skia-harmony.patch::https://git.archlinux.org/svntogit/packages.git/plain/trunk/chromium-skia-harmony.patch?h=packages/chromium'
        'nullptr.patch.base64::https://chromium-review.googlesource.com/changes/chromium%2Fsrc~1552864/revisions/2/patch?download'
        'libcpp.patch.base64::https://chromium-review.googlesource.com/changes/chromium%2Fsrc~1546066/revisions/4/patch?download'
        )
sha256sums=(
            #"$(curl -sL https://gsdview.appspot.com/chromium-browser-official/chromium-${pkgver}.tar.xz.hashes | grep sha256 | cut -d ' ' -f3)"
            "$(curl -sL https://commondatastorage.googleapis.com/chromium-browser-official/chromium-${pkgver}.tar.xz.hashes | grep sha256 | cut -d ' ' -f3)"
            'SKIP'
            'dd2b5c4191e468972b5ea8ddb4fa2e2fa3c2c94c79fc06645d0efc0e63ce7ee1'
            # Patch form Gentoo

            # Misc Patches
            '4b785aeee1cab89bf410de063b7769ef4eb99130888ece60a38a584019747b9f'
            '0d386161052bf8bd3f6c68bdaf766042c75e84db8c3aa356f2e2f8b83511f29f'
            # Patch from crbug (chromium bugtracker) or Arch chromium package
            'd081f2ef8793544685aad35dea75a7e6264a2cb987ff3541e6377f4a3650a28b'
            '5887f78b55c4ecbbcba5930f3f0bb7bc0117c2a41c2f761805fcf7f46f1ca2b3'
            '9a8fc71db40d2749819906041fc0eead2b9326521be898cc150b967b936fcbd3'
            '84a34c48df06ea3cc52bb9ad8e056e68e83a0068c9fce420c3e704091c7203fa'
            )
install=chromium-dev.install

################################################
## -- Don't touch anything below this line -- ##
################################################

# Google API keys (see http://www.chromium.org/developers/how-tos/api-keys)
# NOTE: These are for Arch Linux use ONLY. For your own distribution, please
# get your own set of keys. Feel free to contact foutrelis@archlinux.org for
# more information.
_google_api_key="AIzaSyDwr302FpOSkGRpLlUpPThNTDPbXcIn_FM"
_google_default_client_id="413772536636.apps.googleusercontent.com"
_google_default_client_secret="0ZChLK6AxeA3Isu96MkwqDR4"

# List of third-party components needed for build chromium. The rest is remove by remove_bundled_libraries srcipt in prepare().
_keeplibs=(
           'base/third_party/dmg_fp'
           'base/third_party/dynamic_annotations'
           'base/third_party/icu'
           'base/third_party/nspr'
           'base/third_party/superfasthash'
           'base/third_party/symbolize'
           'base/third_party/valgrind'
           'base/third_party/xdg_mime'
           'base/third_party/xdg_user_dirs'
           'buildtools/third_party/libc++'
           'buildtools/third_party/libc++abi'
           'chrome/third_party/mozilla_security_manager'
           'courgette/third_party'
           'native_client/src/third_party/dlmalloc'
           'native_client_sdk/src/libraries/third_party/newlib-extras'
           'net/third_party/mozilla_security_manager'
           'net/third_party/nss'
           'net/third_party/quic'
           'net/third_party/uri_template'
           'third_party/abseil-cpp'
           'third_party/angle'
           'third_party/angle/src/common/third_party/base'
           'third_party/angle/src/common/third_party/smhasher'
           'third_party/angle/src/common/third_party/xxhash'
           'third_party/angle/src/third_party/compiler'
           'third_party/angle/src/third_party/libXNVCtrl'
           'third_party/angle/src/third_party/trace_event'
           'third_party/angle/third_party/glslang'
           'third_party/angle/third_party/spirv-headers'
           'third_party/angle/third_party/spirv-tools'
           'third_party/angle/third_party/vulkan-headers'
           'third_party/angle/third_party/vulkan-loader'
           'third_party/angle/third_party/vulkan-tools'
           'third_party/angle/third_party/vulkan-validation-layers'
           'third_party/apple_apsl'
           'third_party/axe-core'
           'third_party/blink'
           'third_party/boringssl'
           'third_party/boringssl/src/third_party/fiat'
           'third_party/breakpad'
           'third_party/breakpad/breakpad/src/third_party/curl'
           'third_party/brotli'
           'third_party/cacheinvalidation'
           'third_party/catapult'
           'third_party/catapult/common/py_vulcanize/third_party/rcssmin'
           'third_party/catapult/common/py_vulcanize/third_party/rjsmin'
           'third_party/catapult/third_party/polymer'
           'third_party/catapult/tracing/third_party/d3'
           'third_party/catapult/tracing/third_party/gl-matrix'
           'third_party/catapult/tracing/third_party/jszip'
           'third_party/catapult/tracing/third_party/mannwhitneyu'
           'third_party/catapult/tracing/third_party/oboe'
           'third_party/catapult/tracing/third_party/pako'
           'third_party/ced'
           'third_party/cld_3'
           'third_party/closure_compiler'
           'third_party/crashpad'
           'third_party/crashpad/crashpad/third_party/zlib'
           'third_party/crc32c'
           'third_party/cros_system_api'
           'third_party/dav1d'
           'third_party/devscripts'
           'third_party/dawn'
           'third_party/dom_distiller_js'
           'third_party/emoji-segmenter'
           'third_party/ffmpeg'
           'third_party/flatbuffers'
           'third_party/flot'
           'third_party/glslang'
           'third_party/google_input_tools'
           'third_party/google_input_tools/third_party/closure_library'
           'third_party/google_input_tools/third_party/closure_library/third_party/closure'
           'third_party/googletest'
           'third_party/hunspell'
           'third_party/iccjpeg'
           'third_party/inspector_protocol'
           'third_party/jinja2'
           'third_party/jsoncpp'
           'third_party/jstemplate'
           'third_party/khronos'
           'third_party/leveldatabase'
           'third_party/libXNVCtrl'
           'third_party/libaddressinput'
           'third_party/libaom'
           'third_party/libaom/source/libaom/third_party/vector'
           'third_party/libaom/source/libaom/third_party/x86inc'
           'third_party/libjingle'
           'third_party/libphonenumber'
           'third_party/libsecret'
           'third_party/libsrtp'
           'third_party/libsync'
           'third_party/libudev'
           'third_party/libvpx'
           'third_party/libvpx/source/libvpx/third_party/x86inc'
           'third_party/libwebm'
           'third_party/libwebp'
           'third_party/libxml/chromium'
           'third_party/libyuv'
           'third_party/llvm'
           'third_party/lss'
           'third_party/lzma_sdk'
           'third_party/markupsafe'
           'third_party/mesa'
           'third_party/metrics_proto'
           'third_party/modp_b64'
           'third_party/nasm'
           'third_party/node'
           'third_party/node/node_modules/polymer-bundler/lib/third_party/UglifyJS2'
           'third_party/openmax_dl'
           'third_party/ots'
           'third_party/pdfium'
           'third_party/pdfium/third_party/agg23'
           'third_party/pdfium/third_party/base'
           'third_party/pdfium/third_party/bigint'
           'third_party/pdfium/third_party/freetype'
           'third_party/pdfium/third_party/lcms'
           'third_party/pdfium/third_party/libopenjpeg20'
           'third_party/pdfium/third_party/libpng16'
           'third_party/pdfium/third_party/libtiff'
           'third_party/pdfium/third_party/skia_shared'
           'third_party/perfetto'
           'third_party/ply'
           'third_party/polymer'
           'third_party/protobuf'
           'third_party/protobuf/third_party/six'
           'third_party/pyjson5'
           'third_party/qcms'
           'third_party/rnnoise'
           'third_party/s2cellid'
           'third_party/sfntly'
           'third_party/shaderc'
           'third_party/skia'
           'third_party/skia/include/third_party/vulkan'
           'third_party/skia/third_party/gif'
           'third_party/skia/third_party/skcms'
           'third_party/skia/third_party/vulkan'
           'third_party/smhasher'
           'third_party/spirv-headers'
           'third_party/SPIRV-Tools'
           'third_party/sqlite'
           'third_party/swiftshader'
           'third_party/swiftshader/third_party/llvm-7.0'
           'third_party/swiftshader/third_party/llvm-subzero'
           'third_party/swiftshader/third_party/subzero'
           'third_party/tcmalloc'
           'third_party/unrar'
           'third_party/usrsctp'
           'third_party/vulkan'
           'third_party/web-animations-js'
           'third_party/webdriver'
           'third_party/webrtc'
           'third_party/webrtc/common_audio/third_party/fft4g'
           'third_party/webrtc/common_audio/third_party/spl_sqrt_floor'
           'third_party/webrtc/modules/third_party/fft'
           'third_party/webrtc/modules/third_party/g711'
           'third_party/webrtc/modules/third_party/g722'
           'third_party/webrtc/rtc_base/third_party/base64'
           'third_party/webrtc/rtc_base/third_party/sigslot'
           'third_party/widevine'
           'third_party/woff2'
           'third_party/zlib/google'
           'url/third_party/mozilla'
           'v8/src/third_party/siphash'
           'v8/src/third_party/valgrind'
           'v8/src/third_party/utf8-decoder'
           'v8/third_party/inspector_protocol'
           'v8/third_party/v8'

           # gyp -> gn leftovers.
           'base/third_party/libevent'
           'third_party/adobe'
           'third_party/speech-dispatcher'
           'third_party/usb_ids'
           'third_party/xdg-utils'
           'third_party/yasm/run_yasm.py'
           )

_keeplibs+=(
            'third_party/icu' # https://crbug.com/678661.
            )

# Set build flags.
_flags=(
        "custom_toolchain=\"//build/toolchain/linux/unbundle:default\""
        "host_toolchain=\"//build/toolchain/linux/unbundle:default\""
        'is_debug=false'
        'is_official_build=true'
        'enable_widevine=true'
        'enable_hangout_services_extension=true'
        "ffmpeg_branding=\"ChromeOS\""
        'proprietary_codecs=true'
        "google_api_key=\"${_google_api_key}\""
        "google_default_client_id=\"${_google_default_client_id}\""
        "google_default_client_secret=\"${_google_default_client_secret}\""
        'fieldtrial_testing_like_official_build=true'
        'remove_webcore_debug_symbols=true'
        'use_aura=true'
        'use_gio=false'
        'use_gnome_keyring=false'
        'link_pulseaudio=true'
        'use_sysroot=false'
        'linux_use_bundled_binutils=false'
        'treat_warnings_as_errors=false'
        'enable_nacl=true'
        'enable_nacl_nonsfi=true'
        'use_custom_libcxx=false'
        'use_jumbo_build=false' # https://chromium.googlesource.com/chromium/src/+/lkcr/docs/jumbo.md
#         'jumbo_file_merge_limit=30' # NOTE: test. more than 40 gets OOM in my dual xeon (64Gb ram) machine :/
        'use_vaapi=true'
        'enable_hevc_demuxing=true'
        'enable_ac3_eac3_audio_demuxing=true'
        'enable_mpeg_h_audio_demuxing=true'
        'enable_dolby_vision_demuxing=true'
        'enable_mse_mpeg2ts_stream_parser=true'
        'closure_compile=false'
        'clang_use_chrome_plugins=true'
        'use_gold=false'
        )

if [ "${_wayland}" = "1" ]; then
  _flags+=(
           'use_ozone=true'
           'use_xkbcommon=true'
           'enable_package_mash_services=true'
           'enable_vulkan_wayland_client=true'
           )
fi

# Set the bundled/external components.
# TODO: need ported to GN as GYP doing before. see status page: https://crbug.com/551343.
_use_system=(
#              'ffmpeg'       # I'm not sure why, but all videos stop playback if use system ffmpeg.
             'flac'
             'fontconfig'
             'freetype'
             'harfbuzz-ng'
#              'icu'          # https://crbug.com/678661.
             'libdrm'
#              'libevent'     # Get segfaults and other problems https://bugs.gentoo.org/593458.
             'libjpeg'
             'libpng'
#              'libvpx'       # Needs update.
#              'libwebp'      # Needs update.
             'libxml'
             'libxslt'
             'openh264'
             'opus'
             're2'
             'snappy'
             'yasm'
             'zlib'
             )

# Facilitate deterministic builds (taken from build/config/compiler/BUILD.gn).
CFLAGS+=' -Wno-builtin-macro-redefined'
CXXFLAGS+=' -Wno-builtin-macro-redefined'
CPPFLAGS+=' -D__DATE__=  -D__TIME__=  -D__TIMESTAMP__='

# Conditionals.
if check_option strip y; then
  _flags+=(
           'symbol_level=0'
           )
  # Mimic exclude_unwind_tables=true.
  CFLAGS+=' -fno-unwind-tables -fno-asynchronous-unwind-tables'
  CXXFLAGS+=' -fno-unwind-tables -fno-asynchronous-unwind-tables'
  CPPFLAGS+=' -DNO_UNWIND_TABLES'
fi

if check_buildoption ccache y; then
  # Avoid falling back to preprocessor mode when sources contain time macros.
  export CCACHE_CPP2=yes
  export CCACHE_SLOPPINESS=time_macros
fi

if [ ! -f "${BUILDDIR}/PKGBUILD" ]; then
  _builddir="/${pkgname}"
fi

_clang_path="${BUILDDIR}${_builddir}/src/chromium-${pkgver}/third_party/llvm-build/Release+Asserts/bin/"

export CC="${_clang_path}clang"
export CXX="${_clang_path}clang++"
export AR="${_clang_path}llvm-ar"
export NM=nm
export RANLIB=/usr/bin/true
_lld="ld.lld"


################################################

prepare() {
  cd "${srcdir}/chromium-${pkgver}"

  # Force script incompatible with Python 3 to use /usr/bin/python2.
  sed -i '1s|python$|&2|' \
    -i build/download_nacl_toolchains.py \
    -i build/linux/unbundle/remove_bundled_libraries.py \
    -i build/linux/unbundle/replace_gn_files.py \
    -i tools/clang/scripts/update.py \
    -i third_party/dom_distiller_js/protoc_plugins/json_values_converter.py \
    -i third_party/dom_distiller_js/protoc_plugins/json_values_converter_tests.py \
    -i third_party/ffmpeg/chromium/scripts/build_ffmpeg.py \
    -i third_party/ffmpeg/chromium/scripts/generate_gn.py
  export PNACLPYTHON=/usr/bin/python2

  # Remove most bundled libraries. Some are still needed.
  msg2 "Removing unnecessary components to save disk space."
  build/linux/unbundle/remove_bundled_libraries.py ${_keeplibs[@]} --do-remove

  msg2 "Changing bundle libraries to system ones."
  build/linux/unbundle/replace_gn_files.py --system-libraries ${_use_system[@]}

  msg2 "Setup NaCl/PNaCl SDK: Download and install toolchains"
  build/download_nacl_toolchains.py --packages nacl_x86_newlib,pnacl_newlib,pnacl_translator sync --extract

  msg2 "Download external build components from google"
  tools/clang/scripts/update.py

  # Use chromium-dev as brand name.
  sed -e 's|=Chromium|&-dev|g' \
      -i chrome/app/theme/chromium/BRANDING
  sed -e '0,/output_name = "chrome"/s/= "chrome"/= "chromium-dev"/' \
      -e 's|root_out_dir/chrome"|root_out_dir/chromium-dev"|g' \
      -i chrome/BUILD.gn
  sed -e 's|"chromium-browser"|"chromium-dev"|g' \
      -i media/audio/pulse/pulse_util.cc
  sed -e 's|"Chromium|&-dev|g' \
      -i chrome/common/chrome_constants.cc
  sed -e 's|chromium-browser|chromium-dev|g' \
      -i chrome/browser/shell_integration_linux.cc \
      -i chrome/browser/ui/libgtkui/gtk_util.cc
  sed -e 's|config_dir.Append("chromium|&-dev|' \
      -i chrome/common/chrome_paths_linux.cc
  sed -e 's|/etc/chromium|&-dev|' \
      -e 's|/usr/share/chromium|&-dev|' \
      -i chrome/common/chrome_paths.cc
  sed -e 's|/etc/chromium|&-dev|' \
      -e "s|'app_name': 'Chromium|&-dev|g" \
      -i components/policy/tools/template_writers/writer_configuration.py

  # Fix(?) the name of the sandbox.
  sed -e 's|chrome-sandbox|chrome_sandbox|g'\
      -i sandbox/linux/suid/client/setuid_sandbox_host.cc

  msg2 "Patching the sources"

  # Misc patches.

  # Pats to chromium dev's about why always they forget add/remove missing build rules.
  # Not this time (?).

  # Allow building against system libraries in official builds.
  sed 's|OFFICIAL_BUILD|GOOGLE_CHROME_BUILD|' \
    -i tools/generate_shim_headers/generate_shim_headers.py

  # https://crbug.com/893950.
  sed -e 's/\<xmlMalloc\>/malloc/' \
    -e 's/\<xmlFree\>/free/' \
    -i third_party/blink/renderer/core/xml/*.cc \
    -i third_party/blink/renderer/core/xml/parser/xml_document_parser.cc \
    -i third_party/libxml/chromium/libxml_utils.cc

  # Enable VAAPI.
  patch -p1 -i "${srcdir}/enable-vaapi.patch"
  sed 's|/dri/|/|g' -i media/gpu/vaapi/vaapi_wrapper.cc

  # Patch from crbug (chromium bugtracker) or Arch chromium package.

  # https://crbug.org/819294.
  base64 --decode "${srcdir}/nullptr.patch.base64" | patch -p1 -i -

  # https://crbug.org/947527.
  base64 --decode "${srcdir}/libcpp.patch.base64" | patch -p1 -i -

  # https://crbug.com/skia/6663#c10.
  patch -p0 -i "${srcdir}/chromium-skia-harmony.patch"

  # https://crbug.com/473866.
  patch -p1 -i "${srcdir}/chromium-widevine-r4.patch"

  # Setup nodejs dependency.
  mkdir -p third_party/node/linux/node-linux-x64/bin/
  ln -sf /usr/bin/node third_party/node/linux/node-linux-x64/bin/node

  # Use the file at run time instead of effectively compiling it in.
  sed 's|//third_party/usb_ids/usb.ids|/usr/share/hwdata/usb.ids|g' -i device/usb/BUILD.gn

  # Setup the linker in chromium.
  sed "s|fuse-ld=lld|fuse-ld=${_clang_path}${_lld}|g" -i build/config/compiler/BUILD.gn

  # Setup bundled ffmpeg.
  # Setup the linker in ffmpeg.
  cat "${srcdir}/chromium-ffmpeg-clang.patch" | sed -e "s|__CLANG_PATH__|${_clang_path}|g" -e "s|__LLD__|${_lld}|g" | patch -p1 -i -
  # Disable lto.
  # This avoid messages like:
  # bfd plugin: LLVM gold plugin has failed to create LTO module: Unknown attribute kind (60) (Producer: 'LLVM9.0.0svn' Reader: 'LLVM 8.0.0')
  # when you have installed clang in the system.
  sed 's|--enable-lto|--disable-lto|g' \
      -i third_party/ffmpeg/chromium/scripts/build_ffmpeg.py
  # Use system opus.
  rm -fr third_party/opus/src/include
  ln -sf /usr/include/opus/ third_party/opus/src/include
}

build() {
  msg2 "Build the Launcher"
  make -C chromium-launcher \
    CHROMIUM_SUFFIX="-dev"

  cd "chromium-${pkgver}"

  #echo ${_flags[@]}

  msg2 "Build bundled ffmpeg"
  pushd third_party/ffmpeg &> /dev/null
  chromium/scripts/build_ffmpeg.py linux x64 --branding ChromeOS
  chromium/scripts/copy_config.sh
  chromium/scripts/generate_gn.py
  popd &> /dev/null


  msg2 "Starting building Chromium..."
  LC_ALL=C gn gen out/Release -v --args="${_flags[*]}" --script-executable=/usr/bin/python2

  # Build all.
  # Work around broken deps.
  LC_ALL=C ninja -C out/Release gen/ui/accessibility/ax_enums.mojom{,-shared}.h
  LC_ALL=C ninja -C out/Release -v chrome chrome_sandbox chromedriver
}

package() {
  options=('!strip')

  # Install launcher.
  make -C chromium-launcher \
    PREFIX=/usr \
    CHROMIUM_SUFFIX="-dev" \
    DESTDIR="${pkgdir}" \
    install
  install -Dm644 "chromium-launcher/LICENSE" "${pkgdir}/usr/share/licenses/chromium-dev/LICENSE.launcher"

  pushd "chromium-${pkgver}/out/Release" &> /dev/null

  # Install binaries.
  _bin=(
        'chromium-dev'
        'chrome_sandbox'
        'chromedriver'
        )
  for i in "${_bin[@]}"; do
    case "$i" in
      chrome_sandbox)
        install -Dm4755 "${i}" "${pkgdir}/usr/lib/chromium-dev/${i}"
        ;;
      *)
        install -Dm755 "${i}" "${pkgdir}/usr/lib/chromium-dev/${i}"
        ;;
    esac
  strip $STRIP_BINARIES "${pkgdir}/usr/lib/chromium-dev/${i}"
  done

  ln -sf /usr/lib/chromium-dev/chromedriver "${pkgdir}/usr/bin/chromedriver-dev"

  # Install libs.
  _libs=(
         'libEGL.so'
         'libGLESv2.so'
         'libVkICD_mock_icd.so'
         'libVkLayer_core_validation.so'
         'libVkLayer_object_lifetimes.so'
         'libVkLayer_stateless_validation.so'
         'libVkLayer_thread_safety.so'
         'libVkLayer_unique_objects.so'
         'swiftshader/libEGL.so'
         'swiftshader/libGLESv2.so'
         )
  for i in "${_libs[@]}"; do
    install -Dm755 "${i}" "${pkgdir}/usr/lib/chromium-dev/${i}"
    strip $STRIP_SHARED "${pkgdir}/usr/lib/chromium-dev/${i}"
  done

  _blobs=(
          'natives_blob.bin'
          'snapshot_blob.bin'
          'v8_context_snapshot.bin'
          'icudtl.dat' # https://crbug.com/678661.
          'MEIPreload/manifest.json'
          'MEIPreload/preloaded_data.pb'
          )
  for i in "${_blobs[@]}"; do
    install -Dm644 "${i}" "${pkgdir}/usr/lib/chromium-dev/${i}"
  done

  # Install NaCL.
  _nacl_libs=(
              'nacl_helper'
              'nacl_helper_bootstrap'
              'nacl_helper_nonsfi'
              'nacl_irt_x86_64.nexe'
              )
  for i in "${_nacl_libs[@]}"; do
    install -Dm755 "${i}" "${pkgdir}/usr/lib/chromium-dev/${i}"
    case "$i" in
      nacl_irt_x86_64.nexe)
        ;;
      *)
        strip $STRIP_BINARIES "${pkgdir}/usr/lib/chromium-dev/${i}"
        ;;
    esac
  done

  # Install Resources.
  _resources=(
              'chrome_100_percent.pak'
              'chrome_200_percent.pak'
              'headless_lib.pak'
              'resources.pak'
              'views_mus_resources.pak'
              )
  for i in "${_resources[@]}"; do
    install -Dm644 "${i}" "${pkgdir}/usr/lib/chromium-dev/${i}"
  done

  find resources -type f -name "*" -exec install -Dm644 '{}' "${pkgdir}/usr/lib/chromium-dev/{}" \;

  # Set info.
  source "${srcdir}/chromium-${pkgver}/chrome/installer/linux/common/installer.include"
  PACKAGE=chromium-dev
  PROGNAME=chromium-dev
  MENUNAME="Chromium-dev Web Browser"
  USR_BIN_SYMLINK_NAME=chromium-dev
  # Install .desktop and manpages.
  process_template "${srcdir}/chromium-${pkgver}/chrome/app/resources/manpage.1.in" chromium-dev.1
  install -Dm644 chromium-dev.1 "${pkgdir}/usr/share/man/man1/chromium-dev.1"
  process_template "${srcdir}/chromium-${pkgver}/chrome/installer/linux/common/desktop.template" chromium-dev.desktop
  install -Dm644 chromium-dev.desktop "${pkgdir}/usr/share/applications/chromium-dev.desktop"

  # Install locales.
  find locales -type f -name "*.pak" -exec install -Dm644 '{}' "${pkgdir}/usr/lib/chromium-dev/{}" \;

  # Install icons.
  for _size in 16 22 24 32 48 128 256; do
    case "${_size}" in
      16|32) _branding="${srcdir}/chromium-${pkgver}/chrome/app/theme/default_100_percent/chromium" ;;
      *) _branding="${srcdir}/chromium-${pkgver}/chrome/app/theme/chromium" ;;
    esac
    install -Dm644 "${_branding}/product_logo_${_size}.png" "${pkgdir}/usr/share/icons/hicolor/${_size}x${_size}/apps/chromium-dev.png"
  done
  install -Dm644 "${srcdir}/chromium-dev.svg" "${pkgdir}/usr/share/icons/hicolor/scalable/apps/chromium-dev.svg"

  popd &> /dev/null

  # Install License.
  install -Dm644 "chromium-${pkgver}/LICENSE" "${pkgdir}/usr/share/licenses/chromium-dev/LICENSE"
}
