
from kivy.app import App
from kivy.uix.boxlayout import BoxLayout
from kivy.uix.label import Label
from kivy.uix.image import Image
from kivy.uix.button import Button
from kivy.uix.textinput import TextInput
from kivy.core.window import Window

Window.clearcolor = (0.70, 0.35, 0.35, 1)

class MyApp(App):
    def build(self):
        self.layout = BoxLayout(orientation = 'vertical')

        self.img = Image(source = 'money.png')
        self.layout.add_widget(self.img)

        self.t_text = Label(text = '0', color = '#098000', font_size = 45)
        self.layout.add_widget(self.t_text)

        self.groupMain = BoxLayout()

        self.lefttext = Label(text = 'Конвертация с')
        self.btnUSDwith = Button(text = 'USD')
        self.btnRUBwith = Button(text = 'RUB')
        self.btngroup1 = BoxLayout(orientation = 'vertical')
        self.btngroup1.add_widget(self.lefttext)
        self.btngroup1.add_widget(self.btnUSDwith)
        self.btngroup1.add_widget(self.btnRUBwith)
        self.btnUSDwith.on_press = self.usdwith
        self.btnRUBwith.on_press = self.rubwith
        self.withconevrt = ''

        self.righttext = Label(text = 'Конвертация в')
        self.btnRUBto =Button(text = 'RUB')
        self.btnUSDto = Button(text = 'RUB')
        self.btngroup2 = BoxLayout(orientation = 'vertical')
        self.btngroup2.add_widget(self.righttext)
        self.btngroup2.add_widget(self.btnRUBto)
        self.btngroup2.add_widget(self.btnUSDto)
        self.btnUSDto.on_press = self.usdto
        self.btnRUBto.on_press = self.rubto
        self.toconvert = ''

        self.groupMain.add_widget(self.btngroup1)
        self.groupMain.add_widget(self.btngroup2)

        self.layout.add_widget(self.groupMain)
        self.write_valute = TextInput(size_hint = (1, 0.2))
        self.layout.add_widget(self.write_valute)

        self.btn = Button(text = 'Конвертация', size_hint = (1, 0.2))
        self.layout.add_widget(self.btn)
        self.btn.on_press = self.convert

        return self.layout
    def convert(self):

        if self.withconevrt == 'USD' and self.toconvert == 'RUB':
            self.t_text.text = str(54.20 * float(self.write_valute.text)) + ' RUB'
        elif self.withconevrt == 'USD' and self.toconvert == 'USD':
            self.t_text.text = str(self.write_valute.text) + ' USD'
        elif self.withconevrt == 'RUB' and self.toconvert == 'USD':
            self.t_text.text = str(round(float(self.write_valute.text) / 54.20, 2)) + ' USD'
        elif self.withconevrt == 'RUB' and self.toconvert == 'RUB':
            self.t_text.text = str(self.write_valute.text) + ' RUB'
        else:
            self.t_text.text = 'Перестань а то сломаешь!'

    def usdwith(self):
        self.withconvert = 'USD'
        print('Конвертация с:', self.withconvert)

    def rubwith(self):
        self.withconvert = 'RUB'
        print('Конвертация с:', self.withconvert)

    def usdto(self):
        self.toconvert = 'USD'
        print('Конвертация в:', self.toconvert)

    def rubto(self):
        self.toconvert = 'RUB'
        print('Конвертация в:', self.toconvert)

app = MyApp()
app.run()
