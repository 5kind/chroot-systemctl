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

	cd "${srcdir}/${pkgname}"
	install -Dm 755 "bin/systemctl" -t "${pkgdir}/usr/local/bin/"
	install -Dm 755 "bin/journalctl" -t "${pkgdir}/usr/local/bin/"
	install -Dm 755 "bin/unchroot" -t "${pkgdir}/usr/local/bin/"
	install -Dm 755 "bin/start" -t "${pkgdir}/usr/local/bin/"
	install -Dm 755 "bin/init" -t "${pkgdir}/usr/local/bin/"
	# bin symbolic
	cd "${pkgdir}/usr/local/bin"
	ln -s init  telinit
	ln -s start stop
	ln -s start halt
	ln -s start reboot
	ln -s start shutdown
	ln -s start poweroff
	# licenses
	install -Dm 644 "${srcdir}/EUPL-LICENSE.md" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
	# hook
	install -Dm 644 "${srcdir}/${pkgname}.hook" -t "${pkgdir}"/usr/share/libalpm/hooks/
}
