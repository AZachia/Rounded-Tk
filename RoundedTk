import tkinter as tk
from PIL import Image, ImageTk, ImageDraw




def ShapeImage(color=(255, 255, 255), bg=(255, 255, 255), w=None, h=None, s=100, percent=None):
    new = Image.new('RGBA', (w, h), bg)
    draw = ImageDraw.Draw(new)

    if percent and percent <= 100 and percent >= 0:
        s = (percent / 100) * h / 2

    if s > h or s > w:
        s = w / 2 if h > w else h / 2

    if 2 * s < h:
        draw.rectangle([(0, 0 + s), (w, h - s)], fill=color)
    if 2 * s < w:
        draw.rectangle([(0 + s, 0), (w - s, h)], fill=color)

    draw.pieslice([(0, 0), (s + s, s + s)], start=180, end=270, fill=color)
    draw.pieslice([(w - 2 * s, 0), (w, s * 2)], start=270, end=360, fill=color)
    draw.pieslice([(0, h - 2 * s), (s * 2, h)], start=90, end=180, fill=color)
    draw.pieslice([(w - 2 * s, h - 2 * s), (w, h)], start=0, end=90, fill=color)
    return new


def center_crop(img, new_width=None, new_height=None, crop_methode="center"):
    if type(img) == str:
        img = Image.open(img)
    width, height = img.size
    if crop_methode == 'center':
        if width > height:
            left = (width - height) // 2
            upper = 0
            right = left + height
            bottom = height
            img = img.crop((left, upper, right, bottom))
        elif width < height:
            left = 0
            upper = (height - width) // 2
            right = width
            bottom = upper + width
            img = img.crop((left, upper, right, bottom))

    return img.resize((new_width, new_height))


def con_dict(w):
    options = {}
    for i in w.keys():
        value = w.cget(i)
        options[i] = value.string if type(value) is _tkinter.Tcl_Obj else value
    return options



config_elements = ['height', 'in_', 'variable', 'values', 'indicateon', 'fg', 'takefocus', 'offvalue', 'width', 'xscrollcommand', 'spacing3', 'overrelief', 'date_pattern', 'foreground', 'insertontime', 'tearoff', 'spacing2', 'image', 'spacing1', 'relief', 'tickposition', 'bg', 'to', 'yscrollincrement', 'activeforeground', 'interval', 'from_', 'orient', 'bd', 'selectcolor', 'insertwidth', 'repeatdelay', 'thumb', 'selectforeground', 'tristatevalue', 'labelanchor', 'label', 'value', 'background', 'highlightcolor', 'tickinterval', 'show', 'insertbackground', 'style', 'sliderrelief', 'repeatinterval', 'layout', 'borderwidth', 'labelwidget', 'wraplength', 'in', 'command', 'text', 'anchor', 'state', 'tristateimage', 'activebackground', 'direction', 'troughcolor', 'mode', 'highlightbackground', 'length', 'scrolltype', 'insertofftime', 'highlightthickness', 'wrap', 'onvalue', 'selectborderwidth', 'cursor', 'increment', 'insertborderwidth', 'selectbackground', 'indicatoron', 'resolution', 'underline', 'digits', 'font', 'xscrollincrement', 'padx', 'toggle', 'sliderlength', 'menu', 'justify', 'compound', 'scrollregion', 'insertcursor', 'pady', 'yscrollcommand']

def current_config(widget) -> dict:
    dico = {}
    for k in config_elements:
        try:
            conf = widget[k]
            dico[k] = conf
        except:
            pass
    return dico

   
    


class RoundedWidget:
    def __init__(self, widget, bg='white', cornercolor="red", px=10000, percent=None, time=10):
        self.widget = widget
        self.root = widget.winfo_toplevel()
        self.px = px
        self.bkg = bg
        self.s = px
        self.percent = percent
        self.x = self.widget.winfo_x()
        self.y = self.widget.winfo_y()
        self.w = self.widget.winfo_width()
        self.h = self.widget.winfo_height()
        self.start = True
        self.cornercolor = cornercolor
        self.time = time
        self.root.after(10, self.create)

    def create(self):
        self.s = self.px
        if self.start == True:
            self.x = self.widget.winfo_x()
            self.y = self.widget.winfo_y()
            self.w = self.widget.winfo_width()
            self.h = self.widget.winfo_height()
        self.start = not self.start

        screenshot_tk = ImageTk.PhotoImage(ShapeImage(
            w=self.w, h=self.h, color=self.bkg, bg=self.cornercolor, s=self.s, percent=self.percent))
        try:
            self.widget.config(image=screenshot_tk)
            self.widget.image = screenshot_tk
        except:
            self.widget.create_image(0, 0, image=screenshot_tk, anchor="nw")
            self.widget.image = screenshot_tk

        self.root.after(self.time, self.create)
        
    
    def _hoverenter(self, event=None):
        if self.hovercommand:
            self.hovercommand(*self.hovercommandargs)
        
        self.bkg = self.hoverbg
        self.cornercolor = self.hoverconrnercolor
        self.s = self.hoverpx
        self.percent = self.hoverpercent
        for config in config_elements:
            try:
                self.widget[config] = self.hoverwidgetargs[config]
            except:
                pass


        
    def _hoverleave(self,  event=None):
        self.bkg = self.normalbg
        self.cornercolor = self.normalcornercolor
        self.s = self.normalpx
        self.percent = self.normalpercent
        for config in config_elements:
            try:
                self.widget[config] = self.normalwidgetargs[config]
            except:
                pass

        
        
    def hover(self, command = None, newbg = None, newcornercolor = None, newpx=None, newpercent=None, newwidgetargs = {},commandargs: tuple = ()):
        self.hovercommand = command
        self.hoverbg = newbg or self.bkg
        self.hoverconrnercolor = newcornercolor or self.cornercolor
        self.hoverpx = newpx or self.s
        self.hoverpercent = newpercent or self.percent
        self.hoverwidgetargs = newwidgetargs
        self.hoverwidgetargs = newwidgetargs
        self.hovercommandargs = commandargs
        
        self.normalbg = self.bkg
        self.normalcornercolor = self.cornercolor
        self.normalpercent = self.percent
        self.normalpx = self.s
        self.normalwidgetargs = current_config(self.widget)
        
        self.widget.bind("<Enter>", self._hoverenter)
        self.widget.bind("<Leave>", self._hoverleave)
        
    def click(self, function, args: tuple = ()):
        self.widget.bind("<Button-1>", lambda event, click_args=args: function(click_args))
        
    def _checking(self, event):
        self.checked = not self.checked
        
        if self.checked:
            self.bkg = self.checkedcolor
        else:
            self.bkg = self.normalbg
        
    def create_checkbox(self, cheked=False, checkedcolor = (30, 30, 170)):
        self.checked = cheked
        self.click(self._checking)
        self.checkedcolor = checkedcolor
        self.normalbg = self.bkg

        


        
    def pack(self, *args, **kwargs):
        return self.widget.pack(*args, **kwargs)
    
    def grid(self, *args, **kwargs):
        return self.widget.grid(*args, **kwargs)
    
    





class RoundedWindow(tk.Canvas):
    def __init__(self, root=None, bg='white', color="lightblue", size=10000, percent=None, time: int = 100, image_path=None, crop_methode='center'):
        if root == None:
            root = tk.Tk()
        super().__init__(root)
        self.root = root
        self.time = time
        self.size = size
        self.bkg = bg
        self.percent = percent
        self.last_x, self.last_y, self.last_w, self.last_h = root.winfo_rootx(), root.winfo_rooty(), root.winfo_width(), root.winfo_height()
        self.color = color
        try:
            if self.root.attributes('-transparentcolor'):
                self.color = self.root.attributes('-transparentcolor')
            self.root.attributes('-transparentcolor', self.color)
        except:
            pass
        self.s = size
        self.pack(fill="both", expand=True)
        self.image_path = image_path
        self.time = time
        self.crop_methode = crop_methode
        self.root.after(10, self.create)

    def create(self):
        self.s = self.size
        w = self.root.winfo_width()
        h = self.root.winfo_height()

        test = ShapeImage(w=w, h=h, color=self.bkg, bg=self.color, s=self.s, percent=self.percent)

        if self.image_path and self.image_path != None:
            test3 = center_crop(self.image_path, w, h, crop_methode=self.crop_methode)
            test = Image.alpha_composite(test3.convert('RGBA'), test.convert('RGBA'))

        screenshot_tk = ImageTk.PhotoImage(test)
        self.delete("all")
        self.create_image(0, 0, image=screenshot_tk, anchor="nw")
        self.image = screenshot_tk
        self.root.after(self.time, self.create)

    def mainloop(self):
        return self.root.mainloop()
        
        



###-------------------------------------------------------------------------------------------------


if __name__ == "__main__":
    import ttkbootstrap as ttk
    root = RoundedWindow(ttk.Window(), percent=10)
    
    
    Button = tk.Button(root, text="Boutton example", width=230, height=35, font=(None, 12), compound=tk.CENTER)
    roundedButton = RoundedWidget(Button, bg=(54, 54, 54, 255), percent=100, cornercolor=(255, 255, 255, 255), time=1)
    roundedButton.widget.pack(pady=(50, 0), padx=50)
    
    roundedButton.hover(newbg=(74, 74, 74, 255), newpercent=100, newwidgetargs={"text": "je suis survolé!", "cursor": "hand2"})
    
    Label = tk.Label(root, text="Label example", width=230, height=35, font=(None, 12), compound=tk.CENTER)
    Label["fg"] = "white"
    roundedLabel = RoundedWidget(Label, bg="red", percent=100, cornercolor=(255, 255, 255, 255))
    roundedLabel.hover(newbg=(200, 0, 0, 255), newpercent=30)
    roundedLabel.widget.pack(pady=50)
    
    Entry = tk.Canvas(root, width=230, height=100)
    roundedEntry = RoundedWidget(Entry, bg="red", percent=50,cornercolor=(255, 255, 255, 255))
    roundedEntry.hover(newbg=(200, 0, 0, 255), newpercent=30)
    roundedEntry.widget.pack(pady=50)
    
    Label = tk.Label(root, width=35, height=35, font=(None, 12), compound=tk.CENTER)
    roundedEntry = RoundedWidget(Label, bg=(35, 35, 35, 255), percent=100, cornercolor=(255, 255, 255, 255))
    #roundedEntry.hover(newwidgetargs={"cursor": "hand2"})
    roundedEntry.widget.pack(pady=50)
    
    roundedEntry.create_checkbox()

    root.mainloop()
