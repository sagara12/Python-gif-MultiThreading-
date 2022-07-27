# Python으로 gif 및 Threading 구현
## 요구 기능
* gif 파일을 재생 하는 동안  메인 기능(로그 데이터 기능) 처리
* 메인 기능( 로그 데이터 기능)처리가 끝날 경우 gif 파일을 재생 종료 및 프로그램 종료

## 참조 사이트
* https://deep-eye.tistory.com/23 -> gif 파일을 재생
* https://stackoverflow.com/questions/2905965/creating-threads-in-python -> Threading 기능 구현

## 코드 구현
```Python

        # 메인 화면 라벨 설정
        mainLabel = Label(self.window, text="로그 데이터를 처리중 입니다. 잠시만 기다려 주세요", bg = '#e5e5e5')  # 데이터 베이스 IP 라벨
        mainLabel.place(x=260, y=60)  # mainLabel의 위치

        bottomLabel = Label(self.window, text=" ※ 로그 데이터를 처리가 완료되면 프로그램이 자동으로 종료 됩니다 ", bg='#e5e5e5')  # 데이터 베이스 IP 라벨
        bottomLabel.place(x=220, y=400)  # mainLabel의 위치


        # gif 파일 재생
        frameCnt = 30
        frames = [PhotoImage(file=" gif 파일 경로 ", format='gif -index %i' % (i)) for i in
                  range(frameCnt)]

        # frame을 after메서드를 사용해서 업데이트
        label = Label(self.window, bg = '#e5e5e5')
        label.place(x=300, y=140)



        def update(ind):

            frame = frames[ind]
            ind += 1
            if ind == frameCnt:
                ind = 0
            label.configure(image=frame)
            self.window.after(50, update, ind)

        def main_event_hangdling():

            pythoncom.CoInitialize()

            oj = OptionJudgment()
            oj.option_jud()
            pythoncom.CoInitialize()
            self.window.destroy()

        th1 = Thread(target=main_event_hangdling)
        th1.start()
        self.window.after(0, update, 0)
        self.window.mainloop()
    ```    
