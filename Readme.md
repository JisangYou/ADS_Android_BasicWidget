# ADS04 Android

## 수업 내용

- 기본 위젯들의 사용방법 학습

## Code Review

1. ToggleButton, Switch

```Java
CompoundButton.OnCheckedChangeListener checkedChangeListener
            = new CompoundButton.OnCheckedChangeListener() {
        @Override
        public void onCheckedChanged(CompoundButton compoundButton, boolean check) {
            // 토글, 스위치 처리
            switch (compoundButton.getId()) {
                case R.id.toggleButton:
                    if (check) {
                        textResult.setText("토글버튼이 켜졌습니다");
                    } else {
                        textResult.setText("토글버튼이 꺼졌습니다");
                    }
                    break;
                case R.id.mswitch:
                    if (check) {
                        progress_Bar.setVisibility(View.VISIBLE);
                    } else {
                        progress_Bar.setVisibility(View.INVISIBLE);
                    }
                    break;
            }
        }
    };
```

- compoundButton.getId()로 이벤트가 일어난 위젯을 알 수 있음. 
- setVisibility(View.VISIBLE)은 뷰가 나타나는, setVisibility(View.INVISIBLE)은 뷰가 사라지는 안드로이드 자체적으로 정의되어 있는 Method이다.

2. CheckBox

```Java
 // 체크박스 리스너
    ArrayList<String> checkedList = new ArrayList<>();


    CompoundButton.OnCheckedChangeListener checkboxListner
            = new CompoundButton.OnCheckedChangeListener() {
        @Override
        public void onCheckedChanged(CompoundButton compoundButton, boolean b) {
            // 체크박스 처리
            switch (compoundButton.getId()) { // 아이디 값으로 구분(2개 이상이므로!)
                case R.id.checkDog:
                    if (b) {
                        checkedList.add("개"); // arraylist로 만들어, 만약 체크가 되면 add
                    } else {
                        checkedList.remove("개"); // 아니면 remove
                    }
                    break;
                case R.id.checkPig:
                    if (b) {
                        checkedList.add("돼지");
                    } else {
                        checkedList.remove("돼지");
                    }
                    break;
                case R.id.checkCow:
                    if (b) {
                        checkedList.add("소");
                    } else {
                        checkedList.remove("소");
                    }
                    break;
            }

            String checkedResult = ""; // 초기화를 해줌.
            for (String item : checkedList) {
                checkedResult += item + " ";
            }

            textResult.setText(checkedResult + "(이)가 체크되었습니다.");
        }
    };

```
- 3개의 체크박스가 있고, 체크가 되면 ArrayList에 추가가 되거나 삭제가 되는 이벤트
- 이러한 결과를 향상된 for문으로 꺼내서 textView에 setText해주는 로직

3. RadioGroup, RadioButton

```Java
// 라디오그룹 리스너
    RadioGroup.OnCheckedChangeListener radioListener = new RadioGroup.OnCheckedChangeListener() {
        @Override
        public void onCheckedChanged(RadioGroup radioGroup, @IdRes int radio_id) {
            switch (radio_id) {
                case R.id.radioRed:
                    textResult.setText("빨간불이 켜졌습니다.");
                    break;
                case R.id.radioGreen:
                    textResult.setText("녹색불이 켜졌습니다.");
                    break;
                case R.id.radioBlue:
                    textResult.setText("파란불이 켜졌습니다.");
                    break;

                case R.id.spinner:
                    Intent intent = new Intent(MainActivity.this, SpinnerActivity.class);
                    startActivity(intent);
                    break;
            }
        }
    };
```

- switch (radio_id)에 따라 분기해서 라디오 버튼들을 처리 할 수 있음.
- R.id.spinner을 클릭했을때는 Intent에 의해 다른 Activity로 이동함.
- 해당 Activity는 아래 5. Spinner 참고

4. SeekBar 

```Java
 seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() {
            @Override
            public void onProgressChanged(SeekBar seekBar, int progress, boolean fromUser) {
                seekBarResult.setText(progress + ""); // int 형태로 넘어온 progress를 문자열 형태로 바꿈.
                // 드래그 하는 중에 발생
            }

            @Override
            public void onStartTrackingTouch(SeekBar seekBar) {
                // 최초에 탭하여 드래그 시작할 때 발생
            }

            @Override
            public void onStopTrackingTouch(SeekBar seekBar) {
                // 드래그를 멈출 때 발생
            }
        });
```
- setOnSeekBarChangeListener을 달아줌으로 해서 UI의 상태를 변경을 할 수 있으며, 코드적으로도 상태가 변경됨에 따라 원하는 이벤트를 구현할 수 있다.


5. Spinner

```Java
public class SpinnerActivity extends AppCompatActivity {
    // 1. 스피너에 입력될 데이터를 연결하는 아답터를 정의
    String data[] = {"월","화","수","목","금","토","일"};
   TextView textView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_spinner);

        // 2. 스피너와 데이터를 연결하는 아답터를 정의
        ArrayAdapter<String> adapter = new ArrayAdapter<String>(this, android.R.layout.simple_list_item_1,data);// 아답터 생성

        //3. 아답터와 스피너(리스트)를 연결
        Spinner spinner = (Spinner)findViewById(R.id.spinner);
        spinner.setAdapter(adapter);
        textView = (TextView) findViewById(R.id.textView);

        //4 스피너에 리스너를 달아준다.
        spinner.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
            @Override
            public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {
                String selectedValue = data[position];
                textView.setText(selectedValue);

            }

            @Override
            public void onNothingSelected(AdapterView<?> parent) {

            }
        });
    }
}
```

- 리스너를 달아주고, onItemSelected 메소드에서 int position은 위치값, 즉 String 배열의 아이템 하나의 위치를 나타내는 index이다.
```Java
    String selectedValue = data[position];
                textView.setText(selectedValue);
```
- 이런식으로 spinner에서 클릭 이벤트가 일어났을 때 원하는 값을 TextView에 나타내 줄 수 있다. 

```Java
ArrayAdapter<String> adapter = new ArrayAdapter<String>(this, android.R.layout.simple_list_item_1,data);// 아답터 생성
                                                       //시스템자원, 각 아이템하나의 레이아웃, data들     
// -> ArrayAdapter을 타고 들어가보면
 public ArrayAdapter(@NonNull Context context, @LayoutRes int resource, @NonNull T[] objects) {
        this(context, resource, 0, Arrays.asList(objects));
    } 

```



6. Progress Bar

```Java
        progress_Bar.setVisibility(View.INVISIBLE);  // INVISIBLE -- 화면에 안보이는데 자리는 차지하고 있다
        // VISIBLE   -- 현재 화면에 보이는 상태
        // GONE      -- 화면에서 사라진 상태
```

## 보충설명

![CompoundButton](http://cfile7.uf.tistory.com/image/24573042594724571ADAF5)

- checkBox, RadioButton, ToggleButton, Switch는 CompoundButton의 자식뷰로 아래와 같은 method들을 공통적으로 가지고 있음.

- compoundButton Method
- isChecked() : 체크 유무 상태 확인
- setChecked(boolean checked) : 상태 설정
- setOnCheckedChangeListener(CompoundButton.OnCheckedChangeListener listener) : 리스너 설정
- 등등 많이 있는데, 해당 정보는 안드로이드 사이트에 다 나와 있으며, 필요할 떄 찾아서 사용하면 됨

### Toggle Button

![Toggle](https://developer.android.com/images/ui/togglebutton.png?hl=ko)
- on, off로 이루어진 위젯

### Switch

![Switch](https://developer.android.com/images/ui/switch.png?hl=ko)

- ToggleButton과 유사함
- 좀 더 직관적


### CheckBox

![checkbox](https://developer.android.com/images/ui/checkboxes.png?hl=ko)

- 중복 체크 가능

### RadioGroup, RadioButton

![Radio Button](https://developer.android.com/images/ui/radiobuttons.png?hl=ko)

- 하나의 RadioGroup안에 RadioButton이 존재한다면 중복 Check가 불가능

- RadioButton Api

```Java
void clearCheck()
int getCheckedRadioButtonId()
```



### SeekBar
- 시크바는 ProgressBar를 확장하여 사용자가 터치로 상태를 변경할 수 있도록 한 뷰이다. 
- 시크바는 볼륨 조절이나 화면 밝기 조절 등에 사용할 수 있으며 발생된 이벤트는 SeekBar.OnSeekBarChangeListener 인터페이스를 통해 처리할 수 있다.

```Java
- onStartTrackingTouch()   :  최초에 탭하여 드래그 시작할때 발생
- onProgressChanged() : 드래그 하는 중에 발생
- onStopTrackingTouch() : 드래그를 멈출때 발생

- SeekBar 를 레이아웃에 넣을때
- android:max  는 SeekBar 최대치일때의 수치 설정
- android:thumb 은 SeekBar의 드래그 하는 아이콘 설정
```

### ProgressBar

- "수치 값 또는 작업 진행 상태 표시"라는 공통적인 목적
- 상태를 나타낼 수 있는 widget
- SetVisible을 통해 보여주거나 숨길 수 있음.

### RatingBar

- 평점이나 별점을 줄때 사용하는 widget
- RatingBar.OnRatingBarChangeListener 을 사용하여 변경됬을 때의 상태 값을 알 수 있다.

### Spinner
- Spinner 모양

![spinner](https://developer.android.com/images/ui/spinner.png?hl=ko)

- Spinner와 Adapter의 구조

![adapter](http://cfile29.uf.tistory.com/image/234AF63C58EE221508B10F)

- AdapterView.OnItemSelectedListener 인터페이스와 이에 상응하는 onItemSelected() 콜백 메서드를 구현
- Adapter를 사용하는 위젯
- html의 select와 비슷한 것이다. 여러개 중 하나를 선택 할수 있게 해준다.
- ListView와 마찬가지로 adapter 객체를 이용하여 보여준다





####출처: http://hyunssssss.tistory.com/284 [현's 블로그]
#### 출처: http://recipes4dev.tistory.com/133?category=635576 [개발자를 위한 레시피]
#### 출처: http://aroundck.tistory.com/282 [돼지왕 왕돼지 놀이터]
#### 출처: http://recipes4dev.tistory.com/135 [개발자를 위한 레시피]
#### 출처: http://bitsoul.tistory.com/29 [Happy Programmer~]

## TODO

- 사용법 자체는 어렵지 않으나, 내부적으로 왜 이렇게 구동이 되는지에 대해서 공부가 필요하다.
- spinner의 adapter부분은 추후에 나올 listView와 RecyclerView에서 굉장히 중요하기에, 그때 다시 정리할 것임.

## Retrospect

- TODO에서 처럼 사용법 자체를 익히는데 안주하지 말고, 구동이 되는 원리를 좀더 깊이 있게 연구해봐야 한다. 

## Output
![basicwidget](https://user-images.githubusercontent.com/31605792/34607982-716d0910-f259-11e7-9f21-350fd6816d99.png)