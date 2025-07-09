# OMAR-TV
تطبيق لبث القنوات 
python
import kivy
from kivy.app import App
from kivy.uix.boxlayout import BoxLayout
from kivy.uix.label import Label
from kivy.uix.button import Button
from kivy.uix.spinner import Spinner
from kivy.uix.scrollview import ScrollView
from kivy.uix.gridlayout import GridLayout
from kivy.garden.videoplayer import VideoPlayer

kivy.require('2.0.0')

stream_links = {
    "beIN Sports 1": {
        "عالي": "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8",
        "متوسط": "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8",
        "منخفض": "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8"
},
    "beIN Sports 2": {
        "عالي": "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8",
        "متوسط": "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8",
        "منخفض": "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8"
},
    "beIN Sports 3": {
        "عالي": "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8",
        "متوسط": "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8",
        "منخفض": "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8"
},
    "MBC3": {
        "عالي": "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8",
        "متوسط": "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8",
        "منخفض": "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8"
},
    "2M": {
        "عالي": "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8",
        "متوسط": "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8",
        "منخفض": "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8"
},
    "Abu Dhabi Najijra": {
        "عالي": "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8",
        "متوسط": "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8",
        "منخفض": "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8"
}
}

class OmarTVApp(App):
    def build(self):
        self.selected_quality = "عالي"
        self.root = BoxLayout(orientation='vertical', padding=10, spacing=10)

        self.header = Label(text="📺 مرحبًا بك في OMAR TV *6", font_size=20, size_hint=(1, 0.1))
        self.root.add_widget(self.header)

        nav = BoxLayout(size_hint=(1, 0.1), spacing=10)
        nav.add_widget(Button(text="📅 المباريات", on_press=self.show_matches))
        nav.add_widget(Button(text="📺 القنوات", on_press=self.show_channels))
        self.root.add_widget(nav)

        quality_box = BoxLayout(size_hint=(1, 0.1))
        quality_box.add_widget(Label(text="🎚️ الجودة:", size_hint=(0.3, 1)))
        self.quality_spinner = Spinner(
            text="عالي",
            values=["عالي", "متوسط", "منخفض"],
            size_hint=(0.7, 1)
)
        self.quality_spinner.bind(text=self.set_quality)
        quality_box.add_widget(self.quality_spinner)
        self.root.add_widget(quality_box)

        self.content_list = GridLayout(cols=1, size_hint_y=None, spacing=10, padding=10)
        self.content_list.bind(minimum_height=self.content_list.setter('height'))

        self.scroll = ScrollView(size_hint=(1, 0.7))
        self.scroll.add_widget(self.content_list)
        self.root.add_widget(self.scroll)

        self.show_channels(None)
        return self.root

    def set_quality(self, spinner, text):
        self.selected_quality = text

    def show_channels(self, instance):
        self.content_list.clear_widgets()
        for name in stream_links:
            btn = Button(text=name, font_size=18, size_hint_y=None, height=50)
            btn.bind(on_press=lambda inst, ch=name: self.play_channel(ch))
            self.content_list.add_widget(btn)

    def play_channel(self, channel_name):
        self.content_list.clear_widgets()
        url = stream_links.get(channel_name, {}).get(self.selected_quality)
        if url:
            player = VideoPlayer(source=url, state='play', options={'allow_stretch': True}, size_hint_y=None, height=300)
            self.content_list.add_widget(Label(text=f"📡 البث المباشر: {channel_name} ({self.selected_quality})", font_size=16, size_hint_y=None, height=40))
            self.content_list.add_widget(player)
        else:
[8/‏7 16:56] Microsoft Copilot: self.content_list.add_widget(Label(text="❌ لا يوجد رابط بث لهذه الجودة."))

    def show_matches(self, instance):
        self.content_list.clear_widgets()
        self.content_list.add_widget(Label(
            text="غير متوفر ضد غير متوفر\nالقنوات الناقلة: غير معروف\nالدوري: غير معروف\n⏳ العد التنازلي: 00:00:00",
            font_size=16, size_hint_y=None, height=120
))

if __name__ ==
 '__main__ ':
    OmarTVApp().run()
