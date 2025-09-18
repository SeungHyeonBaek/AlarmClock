# AlarmClock

게임공학전공 백승현

<img width="428" height="883" alt="스크린샷 2025-09-17 오후 12 09 25" src="https://github.com/user-attachments/assets/84674ec1-4716-41d5-8915-be1cf62223c2" />
<img width="428" height="883" alt="스크린샷 2025-09-17 오후 12 10 52" src="https://github.com/user-attachments/assets/c73b8ce9-15e3-4507-9642-19beaca82801" />




### ViewController.swift
~~~
import UIKit

class ViewController: UIViewController {
    
    @IBOutlet weak var lblCurrentTime: UILabel!
    @IBOutlet weak var lblPickerTime: UILabel!
    @IBOutlet var datePicker: UIView!
    
    
    let timeSelecter: Selector = #selector(ViewController.updateTime)
    let interval = 1.0
    var alarmTime: String? //알람이 울릴 시간을 저장하는 alarmTime변수
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        Timer.scheduledTimer(timeInterval: interval, target: self, selector: timeSelecter, userInfo: nil, repeats: true)
    }
    
    
    @IBAction func changeDatePicker(_ sender: UIDatePicker) {
        let datePickerView = sender
        
        let formatter = DateFormatter()
        formatter.dateFormat = "yyyy-MM-dd HH:mm EEE"
        lblPickerTime.text = "선택시간: " + formatter.string(from: datePickerView.date)
        
        alarmTime = formatter.string(from: datePickerView.date) //alarmTime변수에 선택한 시간 저장
    }
    
    @objc func updateTime()
    {
        let date = NSDate()
        
        let formatter = DateFormatter()
        formatter.dateFormat = "yyyy-MM-dd HH:mm EEE"
        lblCurrentTime.text = "현재시간: " + formatter.string(from: date as Date)
        let currentTime = formatter.string(for: date)
        
        if (alarmTime == currentTime) {  //알람시간과 현재시간이 같으면 백그라운드 색상 변경
            view.backgroundColor = UIColor.red
        }
        else {
            view.backgroundColor = UIColor.white
        }
    }
  }
~~~
