<h1 id="custom">Custom</h1>
<h2 id="1-cài-đặt-git-và-golang">1. Cài đặt git và golang</h2>
<pre><code class="language-shell">sudo pacman -S --needed git go
</code></pre>
<h2 id="2-clone-và-cài-đặt-yay">2. Clone và cài đặt yay</h2>
<pre><code class="language-shell">git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
</code></pre>
<h2 id="3-cài-đặt-zsh-và-thay-đổi-shell-mặc-định">3. Cài đặt zsh và thay đổi shell mặc định</h2>
<pre><code class="language-shell">sudo pacman -S zsh
sudo chsh --shell $(which zsh) $USER
</code></pre>
<h2 id="4-cài-đặt-gói-gnome">4. Cài đặt gói Gnome</h2>
<p>Tùy thuộc vào nhu cầu của bạn, bạn có thể cài đặt gói <code>gnome-backgrounds</code> hoặc <code>gnome-shell</code>.
    Nếu bạn muốn có hình nền, hãy chạy lệnh sau:</p>
<pre><code class="language-shell">sudo pacman -S gdm gnome-backgrounds gnome-control-center gnome-keyring
</code></pre>
<p>Nếu bạn không muốn có hình nền(nhẹ hơn chút), hãy chạy lệnh sau:</p>
<pre><code class="language-shell">sudo pacman -S gdm gnome-shell gnome-control-center gnome-keyring
</code></pre>
<p>Sau đó, kích hoạt <a href="https://www.baeldung.com/wp-content/uploads/sites/2/2023/07/gnome_preview.png">GDM</a> để
    có thể đăng nhập với giao diện.:</p>
<pre><code class="language-shell">sudo systemctl enable gdm
</code></pre>
<h2 id="5-cài-đặt-các-gói-bổ-sung">5. Cài đặt các gói bổ sung</h2>
<ul>
    <li>Visual Studio Code:</li>
</ul>
<pre><code class="language-shell">sudo pacman -S code
</code></pre>
<ul>
    <li>Terminal:</li>
</ul>
<pre><code class="language-shell">sudo pacman -S alacritty
</code></pre>
<ul>
    <li>Font <a href="https://www.programmingfonts.org/#jetbrainsmono">Click để xem thử</a>:</li>
</ul>
<pre><code class="language-shell">sudo pacman -S ttf-jetbrains-mono-nerd
</code></pre>
<ul>
    <li>Trình duyệt Google Chrome:</li>
</ul>
<pre><code class="language-shell">yay -Sy google-chrome
</code></pre>
<ul>
    <li>Bộ gõ tiếng Việt:</li>
</ul>
<pre><code class="language-shell">yay -Sy ibus-bamboo
</code></pre>
<p>Sau khi hoàn thành các bước trên, bạn có thể tham khảo hướng dẫn custom giống như MacOS tại <a
        href="https://www.youtube.com/watch?v=VQ6MVky9EUk">đây</a>.</p>
