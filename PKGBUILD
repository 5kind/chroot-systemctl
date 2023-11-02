# Maintainer: 5kind shikabane320@gmail.com

_pkgname=docker-systemctl-replacement
pkgname=chroot-systemctl
pkgver=1932.b18d67e
pkgrel=1
pkgdesc="chroot systemctl replacement - allows to deploy to systemd-controlled containers without starting an actual systemd daemon"
_url='https://github.com/gdraheim/docker-systemctl-replacement'
url='https://github.com/5kind/chroot-systemctl'
arch=('any')
license=('EUPL')
depends=('python' 'sudo' 'iputils')
source=("https://raw.githubusercontent.com/gdraheim/docker-systemctl-replacement/master/EUPL-LICENSE.md"
	"${_pkgname}::git+${_url}"
	"${pkgname}::git+${url}")

b2sums=('7c81e385a62dbee1326de1004377b5dabc4ed795542e5f09dd3d4a381ae25992a36cae90c86a2c785b84a56db807836a70afd49ae9f5f499d601cb72f18074ac'
	'SKIP'
	'SKIP')

install="${srcdir}/${pkgname}.install"

pkgver() {
	cd "${srcdir}/${_pkgname}"
	echo "$(git rev-list --count HEAD).$(git rev-parse --short HEAD)"
}

package() {
	# bin scripts
	cd "${srcdir}/${_pkgname}"
	install -Dm 755 "files/docker/systemctl3.py" -t "${pkgdir}/usr/local/bin/"

	cd "${srcdir}/${pkgname}/bin"
	# systemctl sysvcompat
	install -Dm 755 systemctl -t "${pkgdir}/usr/local/bin/"
	install -Dm 755 journalctl -t "${pkgdir}/usr/local/bin/"
	install -Dm 755 unchroot -t "${pkgdir}/usr/local/bin/"
	install -Dm 755 start -t "${pkgdir}/usr/local/bin/"
	install -Dm 755 init -t "${pkgdir}/usr/local/bin/"
	# android service
	install -Dm 755 android-network-monitor -t "${pkgdir}/usr/local/bin/"
	install -Dm 755 android-start -t "${pkgdir}/usr/local/bin/"
	install -Dm 755 android-stop -t "${pkgdir}/usr/local/bin/"
	install -Dm 755 mount_sdcard -t "${pkgdir}/usr/local/bin/"
	install -Dm 755 switch_sdcard -t "${pkgdir}/usr/local/bin/"
	# bin symbolic
	cd "${pkgdir}/usr/local/bin"
	ln -s init  telinit
	ln -s start stop
	ln -s start halt
	ln -s start reboot
	ln -s start shutdown
	ln -s start poweroff
	# boot preinit
	install -Dm 644 "${srcdir}/${pkgname}/boot/preinit" -t "${pkgdir}/boot/"
	# service
	install -Dm 755 "${srcdir}/${pkgname}/lib/systemd/systemd-networkd-wait-online" -t "${pkgdir}/usr/local/lib/systemd"
	install -Dm 644 "${srcdir}/${pkgname}/etc/systemd/system/android-network-monitor.service" -t "${pkgdir}/etc/systemd/system/"
	install -Dm 644 "${srcdir}/${pkgname}/etc/systemd/system/wait-online@.service" -t "${pkgdir}/etc/systemd/system/"
	# licenses
	install -Dm 644 "${srcdir}/EUPL-LICENSE.md" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
	# hook
	install -Dm 644 "${srcdir}/${pkgname}.hook" -t "${pkgdir}"/usr/share/libalpm/hooks/
}