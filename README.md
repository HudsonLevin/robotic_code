#This code demonstrate how to show location of hand landmark  
import cv2
import mediapipe as mp

Nfing = 5
cap = cv2.VideoCapture(0)

#Call hand pipe line module
mpHands = mp.solutions.hands
hands = mpHands.Hands()
mpDraw = mp.solutions.drawing_utils

while True:
    success, img = cap.read()
    imgRGB = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    results = hands.process(imgRGB)
    #print(results.multi_hand_landmarks)

    if results.multi_hand_landmarks:
        for handLms in results.multi_hand_landmarks:
            for id, lm in enumerate(handLms.landmark):
                h, w, c = img.shape
                cx, cy = int(lm.x * w), int(lm.y * h) --โค้ทของผมตอนใช้งานต้องโชว์นิ้วแบมือให้ขนานกับมุมกล้องนิสนึงนะครับ น่าจะเป็นผลมาจากข้อจำกัดที่ผมใช้แกนXในการอิงตำแหน่งนิ้วครับ--
                if id == 20:                          --สามารถใช้ได้เพียงมือซ้ายด้านเดียวเพราะว่าข้อจำกัดของไลบรารี่ที่ผมเขียนไลบรารี่ข้างขวาเพียงอย่างเดียวครับ--                  
                    id20 = int(id)                      (ผมเขียนสองมือไม่ไหวจริงๆครับ)
                    cx20 = cx                         --วิธีการใช้แบมือและเอานิ้วลงเริ่มตั้งแต่นิ้วโป้งไปนิ้วก้อยครับ และไม่สามารถเอานิ้วลงเรียงจากอีกด้านหรือชูนิ้วชี้นิ้วเดียวได้
                if id == 19:                          --จะมีข้อความแสดงผลที่จอด้านซ้ายว่ามีกี่นิ้วที่ชูอยู่บ้าง และวิธีการอ่านต้องอ่านบรรทัดล่างสุดคือจำนวนนิ้วปัจจุบันที่ชูอยู่ครับ--
                    id19 = int(id)                    --จากสองบรรทัดด้านบนบน ข้อจำกัดเกิดจากการวางเงื่อนไขของif else ที่ผมเขียนไว้--
                    cx19 = cx                           (เพราะผมพยายามจนสมองเบล๋อแล้วเขียนเงื่อนไขของpythonได้แต่แบบนี้จริงๆครับ ผมเขียนแบบให้แสดงคำแยกกันที่ละนิ้วไม่เป็นจริงๆค้าบ 
                if id == 16:                            (T-T) )---
                    id16 = int(id)
                    cx16 = cx
                if id == 15:
                    id15 = int(id)
                    cx15 = cx
                if id == 12:
                    id12 = int(id)
                    cx12 = cx
                if id == 11:
                    id11 = int(id)
                    cx11 = cx
                if id == 8:
                    id8 = int(id)
                    cx8 = cx
                if id == 7:
                    id7 = int(id)
                    cx7 = cx
                if id == 4:
                    id4 = int(id)
                    cx4 = cx
                if id == 3:
                    id3 = int(id)
                    cx3 = cx  
            Nfing = 5  <--เริ่มต้นเซตค่าไว้เป็น5นิ้วก่อนทำเงื่อนไขครับ(หลังผมประกาศNfingอยู่เพราะว่ากันตัวเองงงตอนเขียนครับ)
            cv2.putText(img,"FiveFinger", (10, 70), cv2.FONT_HERSHEY_PLAIN, 3, <---เป็นการกำหนดค่าในการแสดงผลท่หน้าจอว่าให้อยู่จุดไหน
                (255, 0, 255), 3)
            if cx4 > cx3:  <--กำหนดค่ามาร์คตำแหน่งของข้อนิ้ว ให้แยกได้ว่าเอานิ้วไหนลง
                Nfing = 4   โดยเมื่อเอานิ้วลง จุดที่4ชึ่งอยู่ด้านบนของจุดที่3จะมีค่ามากกว่าจุดที่3
                cv2.putText(img,"FourFinger", (10, 140), cv2.FONT_HERSHEY_PLAIN, 3,
                (255, 0, 255), 3)
            if cx8 > cx7 and cx4 > cx3:
                Nfing = 3
                cv2.putText(img,"ThreeFinger", (10, 210), cv2.FONT_HERSHEY_PLAIN, 3,
                (255, 0, 255), 3)
            if cx12 > cx11 and cx8 > cx7 and cx4 > cx3 :
                Nfing = 2
                cv2.putText(img,"TwoFinger", (10, 280), cv2.FONT_HERSHEY_PLAIN, 3,
                (255, 0, 255), 3)
            if cx16 > cx15 and cx12 > cx11 and cx8 > cx7 and cx4 > cx3:
                Nfing = 1 
                cv2.putText(img,"OneFinger", (10, 350), cv2.FONT_HERSHEY_PLAIN, 3,
                (255, 0, 255), 3)       
            if cx20 > cx19 and cx16 > cx15 and cx12 > cx11 and cx8 > cx7 and cx4 > cx3:
                Nfing = 0
                cv2.putText(img,"NoneFinger", (10, 420), cv2.FONT_HERSHEY_PLAIN, 3,
                (255, 0, 255), 3)

             
                                       

            mpDraw.draw_landmarks(img, handLms, mpHands.HAND_CONNECTIONS)

    cv2.imshow("Image", img)
    cv2.waitKey(1)
#Closeing all open windows
#cv2.destroyAllWindows()