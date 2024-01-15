<h1 id="cài-đặt-arch-linux-🐧">Cài đặt Arch Linux 🐧</h1>
<h2 id="chuẩn-bị-🛠️">Chuẩn bị 🛠️</h2>
<h3 id="1-đồng-bộ-hóa-thời-gian-với-hệ-thống-⏰">1. Đồng bộ hóa thời gian với hệ thống ⏰</h3>
<ul>
    <li>Sử dụng các lệnh sau để đồng bộ hóa thời gian và cài đặt múi giờ:</li>
</ul>
<pre><code class="language-bash">timedatectl set-ntp true
timedatectl set-timezone Asia/Ho_Chi_Minh
</code></pre>
<h3 id="2-thiết-lập-kết-nối-internet-🌐">2. Thiết lập kết nối internet 🌐</h3>
<ul>
    <li>Kiểm tra kết nối mạng bằng cách chạy lệnh sau:</li>
</ul>
<pre><code class="language-bash">ping google.com
</code></pre>
<ul>
    <li>Nếu không có kết nối internet, sử dụng các lệnh sau để kết nối với Wi-Fi (<em>đối với mạng dây chỉ cần cắm cáp
            vào thôi</em> 😉):</li>
</ul>
<pre><code class="language-bash">iwctl
device scan
device list
station wlan0 scan
station wlan0 get-networks
station wlan0 connect &quot;tên_wifi&quot;
</code></pre>
<h3 id="3-phân-vùng-ổ-đĩa-📂">3. Phân vùng ổ đĩa 📂</h3>
<ul>
    <li>
        <p>Xác định các phân vùng ổ đĩa bằng lệnh <code>lsblk</code>:</p>
    </li>
    <li>
        <p>Sử dụng công cụ <code>cfdisk</code> để tạo các phân vùng trên ổ đĩa. Đảm bảo rằng bạn tạo ra các phân vùng
            sau đây:</p>
        <ul>
            <li>Phân vùng EFI (<em>phân vùng cho UEFI</em>, <em><strong>không nhớ Legacy có cần hay không nữa, mình quên
                        r =))</strong></em>)</li>
            <li>Phân vùng Swap (<em>không cần thiết nếu bạn dư RAM :|</em>)</li>
            <li>Phân vùng Root (/) (<em>bắt buộc</em>)</li>
            <li>Phân vùng Home (<em>nếu bạn muốn tách riêng phần lưu trữ người dùng</em>)</li>
        </ul>
    </li>
    <li>
        <p>Format các phân vùng</p>
        <ul>
            <li>Hãy thay đổi các phân vùng phù hợp với máy của bạn. Ví dụ: <code>nvme0n1p1</code>,
                <code>nvme0n1p2</code>, <code>nvme0n1p3</code>, <code>nvme0n1p4</code>. 😄</li>
        </ul>
    </li>
</ul>
<pre><code class="language-bash">mkfs.fat -F32 /dev/sda1
mkswap /dev/sda2
mkfs.ext4 /dev/sda3
mkfs.ext4 /dev/sda4
</code></pre>
<ul>
    <li>Mount các phân vùng:</li>
</ul>
<pre><code class="language-bash">swapon /dev/sda2
mount /dev/sda3 /mnt
mkdir /mnt/{boot,home}
mount /dev/sda1 /mnt/boot
mount /dev/sda4 /mnt/home
</code></pre>
<h2 id="cài-đặt-🚀">Cài đặt 🚀</h2>
<ul>
    <li>(Fix lỗi Keyring)</li>
</ul>
<pre><code class="language-bash">pacman -Sy archlinux-keyring
pacman-key --init
pacman-key --populate archlinux
</code></pre>
<h3 id="1-cài-đặt-các-gói-cơ-bản-và-tạo-tệp-fstab-📦">1. Cài đặt các gói cơ bản và tạo tệp Fstab 📦</h3>
<pre><code class="language-bash">pacman -Syyu --noconfirm
pacman -S reflector --noconfirm
reflector --country VN --age 12 --sort rate --save /etc/pacman.d/mirrorlist
pacstrap /mnt linux linux-firmware base base-devel vim
genfstab -U /mnt &gt;&gt; /mnt/etc/fstab
</code></pre>
<h3 id="2-cấu-hình-thiết-lập-cơ-bản-⚙️">2. Cấu hình thiết lập cơ bản ⚙️</h3>
<ul>
    <li>Truy cập vào hệ thống mới:</li>
</ul>
<pre><code class="language-bash">arch-chroot /mnt
</code></pre>
<ul>
    <li>Cấu hình ngôn ngữ hệ thống:<ul>
            <li>Mở tệp <code>locale.gen</code> và bỏ dấu chú thích ngôn ngữ bạn muốn sử dụng:</li>
        </ul>
    </li>
</ul>
<pre><code class="language-bash">vim /etc/locale.gen
locale-gen
</code></pre>
<ul>
    <li>Chỉnh sửa tệp <code>locale.conf</code> bằng <code>vim</code>:</li>
</ul>
<pre><code class="language-bash">vim /etc/locale.conf
LANG=en_US.UTF-8
LANGUAGE=en_US
</code></pre>
<ul>
    <li>Đặt múi giờ:</li>
</ul>
<pre><code class="language-bash">ln -sf /usr/share/zoneinfo/Asia/Ho_Chi_Minh /etc/localtime
hwclock —-systohc
</code></pre>
<h3 id="3-cá-nhân-hóa-hệ-thống-của-bạn-🌟">3. Cá nhân hóa hệ thống của bạn 🌟</h3>
<ul>
    <li>Đặt tên máy chủ:</li>
</ul>
<pre><code class="language-bash">echo tên_của_bạn &gt; /etc/hostname
nvim /etc/hosts
127.0.0.1    localhost.localdomain   localhost
::1          localhost.localdomain   localhost
127.0.1.1    tên_của_bạn.localdomain    tên_của_bạn
</code></pre>
<ul>
    <li>Tạo người dùng mới cho <code>tên_của_bạn</code> và cấu hình người dùng root:</li>
</ul>
<pre><code class="language-bash">useradd -m tên_của_bạnusermod -aG wheel,audio,video,storage,optical,power tên_của_bạn
passwd (nhập mật khẩu của bạn)
passwd tên_của_bạn (nhập mật khẩu của bạn)
EDITOR=vim visudo
(Loại bỏ ký tự &quot;%&quot; trước %wheel ALL=(ALL) NOPASSWD: ALL)
</code></pre>
<ul>
    <li>Cài đặt các gói Arch cần thiết và cấu hình theo ý muốn:</li>
</ul>
<pre><code class="language-bash">pacman -S networkmanager grub os-prober efibootmgr
systemctl enable NetworkManager
</code></pre>
<ul>
    <li>Cài đặt trình khởi động:</li>
</ul>
<pre><code class="language-bash">grub-install --efi-directory=/boot --bootloader-id=arch
grub-mkconfig -o /boot/grub/grub.cfg
</code></pre>
<h2 id="xong-r-đó-khởi-động-lại-và-đăng-nhập-vào-thôi">Xong r đó, khởi động lại và đăng nhập vào thôi</h2>
<pre><code class="language-bash">exit
umount -R /mnt
reboot
</code></pre>
<h2 id="👉-custom"><a href="https://github.com/tripleseven190504/arch/blob/main/CUSTOM.md">👉 Custom</a></h2>
