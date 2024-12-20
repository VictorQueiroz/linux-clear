# Maintainer: JeremyStarTM <jeremystartm@staropensource.de>
# Maintainer: Josip Ponjavic <josipponjavic at gmail dot com>
# Maintainer: JScript Lab <vqueiroz@jscriptlab.com>

### BUILD OPTIONS
# You can modify these settings by executing "env _<setting>=<value> makepkg"
# instead of modifying the PKGBUILD file. Here's an example:
# env _makemenuconfig=y _copyfinalconfig=y _subarch=42 makepkg

# Tweak kernel options prior to a build via menuconfig.
# 
# Set to anything but null to activate.
: "${_makemenuconfig:=""}"

# Tweak kernel options prior to a build via nconfig.
# 
# Set to anything but null to activate.
: "${_makenconfig:=""}"

# Tweak kernel options prior to a build via xconfig.
# 
# Set to anything but null to activate.
: "${_makexconfig:=""}"

# Use the current kernel's .config file
# Enabling this option will use the .config of the currently
# running kernel rather than the Arch Linux defaults. Useful
# when the package gets updated and you already went through
# the trouble of customizing your config options. NOT recommended
# when a new kernel is released, but again, convenient
# for package bumps.
#
# Set to anything but null to activate.
: "${_use_current:=""}"

# Determines whether the kernel configuration should be
# copied into the source tree before compilation starts.
# 
# Set to anything but null to activate.
: "${_copyfinalconfig:=""}"

# Only compile active modules to VASTLY reduce the number
# of modules built and the build time.
# 
# To keep track of which modules are needed for your specific system/hardware,
# give modprobed-db a try: https://aur.archlinux.org/packages/modprobed-db
# 
# More at this wiki page ---> https://wiki.archlinux.org/index.php/Modprobed-db
# Set to anything but null to activate.
: "${_localmodcfg:=""}"

# Optionally select a sub architecture by number or
# leave blank, which will require user interaction during the build.
# Note that the default option is 40.
#
#  1. AMD Opteron/Athlon64/Hammer/K8 (MK8)
#  2. AMD Opteron/Athlon64/Hammer/K8 with SSE3 (MK8SSE3)
#  3. AMD 61xx/7x50/PhenomX3/X4/II/K10 (MK10)
#  4. AMD Barcelona (MBARCELONA)
#  5. AMD Bobcat (MBOBCAT)
#  6. AMD Jaguar (MJAGUAR)
#  7. AMD Bulldozer (MBULLDOZER)
#  8. AMD Piledriver (MPILEDRIVER)
#  9. AMD Steamroller (MSTEAMROLLER)
#  10. AMD Excavator (MEXCAVATOR)
#  11. AMD Zen (MZEN)
#  12. AMD Zen 2 (MZEN2)
#  13. AMD Zen 3 (MZEN3)
#  14. AMD Zen 4 (MZEN4)
#  15. Intel P4 / older Netburst based Xeon (MPSC)
#  16. Intel Core 2 (MCORE2)
#  17. Intel Atom (MATOM)
#  18. Intel Nehalem (MNEHALEM)
#  19. Intel Westmere (MWESTMERE)
#  20. Intel Silvermont (MSILVERMONT)
#  21. Intel Goldmont (MGOLDMONT)
#  22. Intel Goldmont Plus (MGOLDMONTPLUS)
#  23. Intel Sandy Bridge (MSANDYBRIDGE)
#  24. Intel Ivy Bridge (MIVYBRIDGE)
#  25. Intel Haswell (MHASWELL)
#  26. Intel Broadwell (MBROADWELL)
#  27. Intel Skylake (MSKYLAKE)
#  28. Intel Skylake X (MSKYLAKEX)
#  29. Intel Cannon Lake (MCANNONLAKE)
#  30. Intel Ice Lake (MICELAKE)
#  31. Intel Cascade Lake (MCASCADELAKE)
#  32. Intel Cooper Lake (MCOOPERLAKE)
#  33. Intel Tiger Lake (MTIGERLAKE)
#  34. Intel Sapphire Rapids (MSAPPHIRERAPIDS)
#  35. Intel Rocket Lake (MROCKETLAKE)
#  36. Intel Alder Lake (MALDERLAKE)
#  37. Intel Raptor Lake (MRAPTORLAKE)
#  38. Intel Meteor Lake (MMETEORLAKE)
#  39. Intel Emerald Rapids (MEMERALDRAPIDS)
#  40. Generic-x86-64 (GENERIC_CPU)
#  41. Generic-x86-64-v2 (GENERIC_CPU2)
#  42. Generic-x86-64-v3 (GENERIC_CPU3)
#  43. Generic-x86-64-v4 (GENERIC_CPU4)
#  44. Intel-Native optimizations autodetected by the compiler (MNATIVE_INTEL)
#  45. AMD-Native optimizations autodetected by the compiler (MNATIVE_AMD)
: "${_subarch:=""}"

# Enable compilation with LLVM
# Be warned, this is largely untested by me (JeremyStarTM). It *should* work,
# but if it doesn't, write a comment and I'll fix it.
# 
# Set to anything but null to activate.
: "${_use_llvm_lto:=""}"

# Debug options
# This allows you to enable or disable debug options.
# Set to 'y' to force enable, 'n' to force disable or '' to ignore debug options.
# Leaving the setting empty will use the kernel configuration setting to determine
# if debug options shall be enabled/disabled.
# 
# Set to anything but null to activate.
: "${_debug:=""}"

# Make job count
# This allows us to specify the number that should be given to the `-j` argument of the `make` command.
: "${_make_jobs:="n"}"

# Make all
# Whether to run `make all` or just `make`
: "${_make_all:=1}"

# ZSTD Clevel
: "${_zstd_clevel:=19}"

### BUILD OPTIONS END

# Kernel version
_kernel_major=6.10
_kernel_minor=7
# Clear Linux patches version
_clr=7-1460
# kernel_compiler_patch version
_kernelcompilerpatch="20240221.2"
# Source directory names
_src_linux=linux-${_kernel_major}
_src_clr=${_kernel_major}.${_clr}

# Package information
pkgbase=linux-clear-thinkcentre-m70q
pkgver=${_kernel_major}.${_kernel_minor}
pkgrel=1
pkgdesc="Linux kernel with patches from Clear Linux which allow for higher performance."
arch=("x86_64")
url="https://github.com/clearlinux-pkgs/linux"
license=(GPL-2.0-only)
makedepends=("bc" "cpio" "gettext" "git" "libelf" "pahole" "perl" "python" "tar" "xz" "zstd")
[[ -n "${_use_llvm_to}" ]] && makedepends+=("clang" "llvm" "lld")
options=("!strip" "!debug")
[[ "${_debug}" == "y" ]] && options=("!strip")
source=(
  "https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-${_kernel_major}.tar.xz"
  "https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-${_kernel_major}.tar.sign"
  "https://cdn.kernel.org/pub/linux/kernel/v6.x/patch-${_kernel_major}.${_kernel_minor}.xz"
  "cl-linux::git+https://github.com/clearlinux-pkgs/linux.git#tag=${_src_clr}"
  "more-uarches-${_kernelcompilerpatch}.tar.gz::https://github.com/graysky2/kernel_compiler_patch/archive/${_kernelcompilerpatch}.tar.gz"
)

[[ -n "${_use_llvm_lto}" ]] && BUILD_FLAGS=("LLVM=1" "LLVM_IAS=1")

export KBUILD_BUILD_HOST=archlinux
export KBUILD_BUILD_USER=${pkgbase}
export KBUILD_BUILD_TIMESTAMP="$(date -Ru${SOURCE_DATE_EPOCH:+d @$SOURCE_DATE_EPOCH})"

prepare() {
    cd "${_src_linux}" || exit 1
    
    # Patch with kernel version patches
    patch -Np1 -i ../patch-${_kernel_major}.${_kernel_minor} || true
    
    # Set version
    echo "-${pkgrel}" > localversion.10-pkgrel
    echo "${pkgbase#linux}" > localversion.20-pkgname
    
    # Patch with Clear Linux patches
    for i in $(grep '^Patch' "${srcdir}"/cl-linux/linux.spec|grep -Ev '^Patch0132|^Patch0109|^Patch0118|^Patch0113|^Patch0138|^Patch0139|^Patch0147' | sed -n 's/.*: //p'); do
        if [ -n "${_use_llvm_lto}" ]; then
            if [ "${i}" == "0133-novector.patch" ] ; then
                continue
            fi
        fi
        
        patch -Np1 -i "${srcdir}/cl-linux/${i}" || true
    done
    
    # Copy configuration file (if found)
    if [ -f "${startdir}/kconfig" ]; then
        echo ":: Using configuration file \"${startdir}/kconfig\""
        cp -Tf "${startdir}/kconfig" ./.config
    else
        echo ":: Using configuration file \"${srcdir}/${pkgbase}/config\""
        cp -Tf $srcdir/cl-linux/config ./.config
    fi
    
    # Extra configuration
    # General setup
    scripts/config --set-str DEFAULT_HOSTNAME archlinux \
                   -e IKCONFIG \
                   -e IKCONFIG_PROC \
                   -u RT_GROUP_SCHED
    # Power management and ACPI options
    scripts/config -e ACPI_REV_OVERRIDE_POSSIBLE \
                   -e ACPI_TABLE_UPGRADE
    # Virtualization
    scripts/config -e KVM_SMM
    # General architecture-dependent options
    scripts/config -e KPROBES
    # Enable loadable module support
    scripts/config -u MODULE_SIG_FORCE
    # Networking support
    scripts/config -e NETFILTER_INGRESS
    # Device Drivers
    scripts/config -e FRAMEBUFFER_CONSOLE_DEFERRED_TAKEOVER \
                   -e DELL_SMBIOS_SMM \
                   -m PATA_JMICRON \
                   -E SOUND SOUND_OSS_CORE \
                   -e SND_OSSEMUL \
                   -M SND_OSSEMUL SND_MIXER_OSS \
                   -M SND_MIXER_OSS SND_PCM_OSS \
                   -E SND_PCM_OSS SND_PCM_OSS_PLUGINS \
                   -m AGP -M AGP AGP_INTEL -M AGP_INTEL AGP_VIA
    # Kernel hacking -> Compile-time checks and compiler options -> Make section mismatch errors non-fatal
    scripts/config -e SECTION_MISMATCH_WARN_ONLY
    # File systems
    scripts/config -m NTFS3_FS \
                   -e NTFS3_LZX_XPRESS \
                   -e NTFS3_FS_POSIX_ACL
    scripts/config -m SMB_SERVER \
                   -e SMB_SERVER_SMBDIRECT \
                   -e SMB_SERVER_CHECK_CAP_NET_ADMIN \
                   -e SMB_SERVER_KERBEROS5
    # Security options
    scripts/config -e SECURITY_SELINUX \
                   -e SECURITY_SELINUX_BOOTPARAM \
                   -e SECURITY_SMACK \
                   -e SECURITY_SMACK_BRINGUP \
                   -e SECURITY_SMACK_NETFILTER \
                   -e SECURITY_SMACK_APPEND_SIGNALS \
                   -e SECURITY_TOMOYO \
                   -e SECURITY_APPARMOR \
                   -e SECURITY_YAMA
    # Library routines
    scripts/config -k -e FONT_TER16x32
    
    # Enable LLVM compilation
    [[ -n "${_use_llvm_lto}" ]] && scripts/config -d LTO_NONE \
                                                  -e LTO \
                                                  -e LTO_CLANG \
                                                  -e ARCH_SUPPORTS_LTO_CLANG \
                                                  -e ARCH_SUPPORTS_LTO_CLANG_THIN \
                                                  -e HAS_LTO_CLANG \
                                                  -e LTO_CLANG_THIN \
                                                  -e HAVE_GCC_PLUGINS
    
    # Enable or disable debug settings
    [[ "${_debug}" == "y" ]] && scripts/config -e DEBUG_INFO \
                                               -e DEBUG_INFO_BTF \
                                               -e DEBUG_INFO_DWARF4 \
                                               -e PAHOLE_HAS_SPLIT_BTF \
                                               -e DEBUG_INFO_BTF_MODULES
    [[ "${_debug}" == "n" ]] && scripts/config -d DEBUG_INFO \
                                               -d DEBUG_INFO_BTF \
                                               -d DEBUG_INFO_DWARF4 \
                                               -d PAHOLE_HAS_SPLIT_BTF \
                                               -d DEBUG_INFO_BTF_MODULES
    
    # Run olddefconfig
    make ${BUILD_FLAGS[*]} olddefconfig
    diff -u $srcdir/cl-linux/config .config || :
    
    # Patch with kernel_compiler_patch patches
    # This must be executed after olddefconfig
    # to allow for the next section to run.
    patch -Np1 -i "$srcdir/kernel_compiler_patch-$_kernelcompilerpatch/more-uarches-for-kernel-6.8-rc4+.patch"
    
    # Set subarch automatically
    [[ -n "${_subarch}" ]] && yes "${_subarch}" | make ${BUILD_FLAGS[*]} oldconfig
    # Ask for subarch
    [[ -z "${_subarch}" ]] && make ${BUILD_FLAGS[*]} oldconfig
    
    # Optionally use the configuration of the running kernel
    # Written originally by nous, see
    # https://web.archive.org/web/20110711231356/https://aur.archlinux.org/packages.php?ID=40191 (package doesn't exist anymore)
    [[ -n "${_use_current}" ]] &&
        if [[ -s /proc/config.gz ]]; then
            # modprobe configs
            zcat /proc/config.gz > ./.config
        else
            warning "Your kernel was not compiled with IKCONFIG_PROC."
            warning "Unable to read kernel configuration, aborting."
            exit
        fi
    
    # Read and apply modprobed database
    # See https://aur.archlinux.org/packages/modprobed-db
    [[ -n "${_localmodcfg}" ]] &&
        if [ -e "${HOME}/.config/modprobed.db" ]; then
            make ${BUILD_FLAGS[*]} LSMOD=${HOME}/.config/modprobed.db localmodconfig
        else
            echo ":: No modprobed.db file was found at ${HOME}/.config, skipping"
        fi
    
    # Write kernel version
    make -s kernelrelease > version
    
    # Open configuration editors
    [[ -n "$_makemenuconfig" ]] && make ${BUILD_FLAGS[*]} menuconfig
    [[ -n "$_makexconfig" ]] && make ${BUILD_FLAGS[*]} xconfig
    [[ -n "$_makenconfig" ]] && make ${BUILD_FLAGS[*]} nconfig

    # Save configuration
    [[ -n "${_copyfinalconfig}" ]] && cp -Tf ./.config "${startdir}/kconfig-new" || true
}

build() {
    cd "${_src_linux}" || exit 1
    MAKE_ARGUMENTS=${BUILD_FLAGS[*]}
    [[ "${_make_jobs}" != "n" ]] && MAKE_ARGUMENTS="${MAKE_ARGUMENTS} -j ${_make_jobs}"
    [[ "${_make_all}" == "n" ]] && MAKE_ARGUMENTS="${MAKE_ARGUMENTS} all"
    echo "Running make with the following arguments:"
    echo "${MAKE_ARGUMENTS}"
    make ${MAKE_ARGUMENTS}
}


_package() {
    pkgdesc="${pkgdesc} This package includes the kernel and compiled modules."
    depends=("coreutils" "kmod" "initramfs")
    optdepends=("wireless-regdb: to set the correct wireless channels of your country"
                "linux-firmware: firmware images needed for some devices")
    provides=(VIRTUALBOX-GUEST-MODULES WIREGUARD-MODULE KSMBD-MODULE)
    install=linux.install
    
    cd "${_src_linux}" || exit 1
    local modulesdir="${pkgdir}/usr/lib/modules/$(<version)"
    
    # Create boot image
    # systemd expects to find the kernel there to allow hibernation
    # https://github.com/systemd/systemd/commit/edda44605f06a41fb86b7ab8128dcf99161d2344
    install -Dm644 "$(make -s image_name)" "${modulesdir}/vmlinuz"
    
    # Used by mkinitcpio to name the kernel
    echo "${pkgbase}" | install -Dm644 /dev/stdin "${modulesdir}/pkgbase"
    
    # Install modules
    MAKE_ARGUMENTS="${BUILD_FLAGS[*]} INSTALL_MOD_PATH="${pkgdir}/usr" INSTALL_MOD_STRIP=1 DEPMOD=/doesnt/exist"
    [[ "${_make_jobs}" != "n" ]] && MAKE_ARGUMENTS="${MAKE_ARGUMENTS} -j ${_make_jobs}"
    [[ "${_zstd_clevel}" != "n" ]] && ZSTD_CLEVEL="${_zstd_clevel}" make ${MAKE_ARGUMENTS} modules_install  # Suppress depmod
    [[ "${_zstd_clevel}" == "n" ]] && make ${MAKE_ARGUMENTS} modules_install  # Suppress depmod
    
    # Remove build directory
    rm "${modulesdir}"/build
}

_package-headers() {
    pkgdesc="${pkgdesc} This package includes header files and scripts for building kernel modules."
    depends=("pahole")
    
    cd "${_src_linux}" || exit 1
    local builddir="${pkgdir}/usr/lib/modules/$(<version)/build"
    
    install -Dt "${builddir}" -m644 .config Makefile Module.symvers System.map \
        localversion.* version vmlinux
    install -Dt "${builddir}/kernel" -m644 kernel/Makefile
    install -Dt "${builddir}/arch/x86" -m644 arch/x86/Makefile
    cp -t "${builddir}" -a scripts
    
    # Required when STACK_VALIDATION is enabled
    install -Dt "${builddir}/tools/objtool" tools/objtool/objtool
    
    # Required when DEBUG_INFO_BTF_MODULES is enabled
    [[ -f tools/bpf/resolve_btfids/resolve_btfids ]] && install -Dt "${builddir}/tools/bpf/resolve_btfids" tools/bpf/resolve_btfids/resolve_btfids
    
    cp -t "${builddir}" -a include
    cp -t "${builddir}/arch/x86" -a arch/x86/include
    install -Dt "${builddir}/arch/x86/kernel" -m644 arch/x86/kernel/asm-offsets.s
    
    install -Dt "${builddir}/drivers/md" -m644 drivers/md/*.h
    install -Dt "${builddir}/net/mac80211" -m644 net/mac80211/*.h
    
    # https://bugs.archlinux.org/task/13146
    install -Dt "${builddir}/drivers/media/i2c" -m644 drivers/media/i2c/msp3400-driver.h
    
    # https://bugs.archlinux.org/task/20402
    install -Dt "${builddir}/drivers/media/usb/dvb-usb" -m644 drivers/media/usb/dvb-usb/*.h
    install -Dt "${builddir}/drivers/media/dvb-frontends" -m644 drivers/media/dvb-frontends/*.h
    install -Dt "${builddir}/drivers/media/tuners" -m644 drivers/media/tuners/*.h
    
    # https://bugs.archlinux.org/task/71392
    install -Dt "${builddir}/drivers/iio/common/hid-sensors" -m644 drivers/iio/common/hid-sensors/*.h
    
    find . -name 'Kconfig*' -exec install -Dm644 {} "${builddir}/{}" \;
    
    # Remove redundant architectures
    local arch
    for arch in "${builddir}"/arch/*/; do
        [[ $arch = */x86/ ]] && continue
        echo "Removing $(basename "${arch}")"
        rm -r "${arch}"
    done
    
    # Remove documentation
    rm -r "${builddir}/Documentation"
    
    # Remove broken symlinks
    find -L "${builddir}" -type l -printf "Removing %P\n" -delete
    
    # Remove loose objects
    find "${builddir}" -type f -name '*.o' -printf "Removing %P\n" -delete
    
    # Strip build tools
    local file
    while read -rd "" file; do
        case "$(file -Sib "$file")" in
            application/x-sharedlib\;*)      # Libraries (.so)
                strip -v $STRIP_SHARED "$file" ;;
            application/x-archive\;*)        # Libraries (.a)
                strip -v $STRIP_STATIC "$file" ;;
            application/x-executable\;*)     # Binaries
                strip -v $STRIP_BINARIES "$file" ;;
            application/x-pie-executable\;*) # Relocatable binaries
                strip -v $STRIP_SHARED "$file" ;;
        esac
    done < <(find "${builddir}" -type f -perm -u+x ! -name vmlinux -print0)
    
    # Strip vmlinux
    strip -v $STRIP_STATIC "${builddir}/vmlinux"
    
    # Add symlink to build directory
    mkdir -p "$pkgdir/usr/src"
    ln -sr "${builddir}" "$pkgdir/usr/src/$pkgbase"
}

pkgname=("$pkgbase" "$pkgbase-headers")
for _p in "${pkgname[@]}"; do
  eval "package_$_p() {
    $(declare -f "_package${_p#$pkgbase}")
    _package${_p#$pkgbase}
  }"
done
validpgpkeys=(
  "ABAF11C65A2970B130ABE3C479BE3E4300411886"  # Linus Torvalds
  "647F28654894E3BD457199BE38DBBDC86092693E"  # Greg Kroah-Hartman
  "9B55E409B90ACFA478D1048B11F72643EBF1E972"  # JScript Lab
)
sha256sums=("774698422ee54c5f1e704456f37c65c06b51b4e9a8b0866f34580d86fef8e226"
            "SKIP"
            "221b40140dabf32b1dcecee374d1733e4566e52da5313909d70808aa8e8ad9c0"
            "SKIP"
            "1d3ac3e581cbc5108f882fcdc75d74f7f069654c71bad65febe5ba15a7a3a14f")
