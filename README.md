سلام عليكم
شرح طريقة تغيير mac address
مع تشغيل النظام

تحميل الاداة 
sudo apt install macchanger

معرفة mac addrees 
macchanger -s 
بعد 
s
تحط اسم كرت الشبكة

يمديك تبحث عن الاداة وتشوف شرح لها

إنشاء ملف 
sudo touch /etc/systemd/system/changemac@.service
بعدها
gedit admin:///etc/systemd/system/changemac@.service

داخل الملف هاذا
changemac@.service
تضيف هاذي
_________________________________

[Unit]
Description=changes mac for %I
Wants=network.target
Before=network.target
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
Type=oneshot
ExecStart=/usr/bin/macchanger -r %I
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
______________________________________
وتحفظ الملف
بعدها تضيف الامر هاذا عشان يشتغل الملف مع التشغيل

sudo systemctl enable changemac@enp10s0.service
بعد @ تضيف اسم كرت الشبكة حقتك وبكذا 
ان شاء الله راح يشتغل معك 

واذا اردت الغاء تشغيل الملف مع التشغيل
sudo systemctl disable changemac@enp10s0.service
وبعد @ اضف كرت الشبكة
وشكرا

المصدر

https://www.linuxuprising.com/2018/05/how-to-permanently-change-mac-address.html
