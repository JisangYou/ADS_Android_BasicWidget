# 위젯 사용법
## 위젯 리스너 형태
```Java

      toggleButton.setOnCheckedChangeListener(checkedChangeListener); // setOnCheckedChangeListener를 달아 주어 처리해준다.
      mswitch.setOnCheckedChangeListener(checkedChangeListener);
      checkDog.setOnCheckedChangeListener(checkboxListner);
      checkPig.setOnCheckedChangeListener(checkboxListner);
      checkCow.setOnCheckedChangeListener(checkboxListner);
      radioGroup.setOnCheckedChangeListener(radioListener);
      progress_Bar.setVisibility(View.INVISIBLE);  // INVISIBLE -- 화면에 안보이는데 자리는 차지하고 있다
      // VISIBLE   -- 현재 화면에 보이는 상태
      // GONE      -- 화면에서 사라진 상태
```
## 토글, 스위치
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

## 체크박스
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
                       checkedList.add("개"); // arraylist로 만들고, 만약 체크가 되면 add
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

           String checkedResult = ""; // 초기화를 해주어야함!
           for (String item : checkedList) { //체크박스는 중복이 가능하므로
               checkedResult += item + " "; //for문을 돌려 표현해준다.
           }

           textResult.setText(checkedResult + "(이)가 체크되었습니다.");
       }
   };
```

## 라디오그룹 및 라디오 버튼
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

             }
       }
   };
```

## seekbar
```Java
seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() {
         @Override
         public void onProgressChanged(SeekBar seekBar, int progress, boolean fromUser) {
             seekBarResult.setText(progress + ""); // int 형태로 넘어온 progress를 문자열 형태로 바꿈.
         }

         @Override
         public void onStartTrackingTouch(SeekBar seekBar) {

         }

         @Override
         public void onStopTrackingTouch(SeekBar seekBar) {
         }
     });
```
