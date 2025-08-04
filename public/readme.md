# AIOT
## AIOT 로봇 융합 스마트제조 실무
-----------------------------------------------------------------
## 파이썬을 이용한 간단한 스톱워치
---------------------------------------------------------
import tkinter as tk
import time

class Stopwatch:
    def __init__(self, root):
        self.root = root
        self.running = False
        self.start_time = 0
        self.elapsed_time = 0

        self.label = tk.Label(root, text="00:00:00", font=("Courier", 40))
        self.label.pack(pady=20)

        self.start_btn = tk.Button(root, text="▶ 시작", width=15, command=self.start)
        self.start_btn.pack(pady=5)

        self.stop_btn = tk.Button(root, text="⏸ 정지", width=15, command=self.stop)
        self.stop_btn.pack(pady=5)

        self.reset_btn = tk.Button(root, text="🔁 리셋", width=15, command=self.reset)
        self.reset_btn.pack(pady=5)

        self.update_timer()

    def update_timer(self):
        if self.running:
            self.elapsed_time = time.time() - self.start_time
        minutes = int(self.elapsed_time // 60)
        seconds = int(self.elapsed_time % 60)
        millis = int((self.elapsed_time - int(self.elapsed_time)) * 100)
        self.label.config(text=f"{minutes:02}:{seconds:02}:{millis:02}")
        self.root.after(50, self.update_timer)

    def start(self):
        if not self.running:
            self.start_time = time.time() - self.elapsed_time
            self.running = True

    def stop(self):
        if self.running:
            self.running = False

    def reset(self):
        self.running = False
        self.elapsed_time = 0

if __name__ == "__main__":
    root = tk.Tk()
    root.title("⏱️ 스톱워치")
    root.geometry("300x300")
    Stopwatch(root)
    root.mainloop()

-----------------------------------------------------------------

