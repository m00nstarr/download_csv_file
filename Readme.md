
제작자 : 이문형 / 캘커타 커뮤니케이션즈 인턴
연락처 : moonstar114@naver.com
제작일 : 20/07/16

description : CMS로부터 원하는 기간, 타입을 선택하여 다운로드 받을 수 있는 자동화 툴입니다.


** 주의 사항 **
1. 크롬 브라우저를 연 상태가 아니여야 합니다.
2. 브라우저를 다 닫았을때 로그인 유지가 되지 않아야 합니다. (중요)
3. 다운로드를 모두 받기 전까지 다른 조작이 없어야 합니다.

** 환경 **
1. 크롬 브라우저 
2. 크롬 - 설정 - 고급 - 다운로드 전에 각 파일의 저장 위치 확인 (체크 해제) 


** 사용법 **

1. download_file.xaml 파일을 실행합니다.

2.  create_folder에서 "C:\Users\moons\Desktop\" 이부분을 -> "원하는 다운 디렉토리" (큰 따옴표 포함) 으로 커스텀
총 두군데 수정 ) create folder를 누르고 각각 왼쪽 오른쪽의 Sequence들을 더블 클릭한 후 Assign 칸의 directory name을 바꾼다.

3. 파일 디버그를 통해 실행


Input Date 은 원하는 날짜를 입력받는 process 입니다.
다이얼로그로 “Press date type ( D/ W/ M)” 과 함께 시작하며 D는 daily, W는 weekly, M은 monthly 를 의미합니다. 현재는 M만 구현이 되었고 M이 아니면 다시 입력 받게 되어있습니다.
그리고 start_date 와 end_date를 입력하는 과정이 있습니다.
현재는 end_date가 start_date보다 뒤의 날짜인지 검증하는 과정이 없습니다. 

2.
select type은 원하는 OS와 os별 카테고리를 택하는 과정입니다.
먼저 country를 물어봅니다. country를 택하고, 뒤에 3번 과정 create_folder에서 디렉토리 이름이 길어지는 것을 방지하기 위하여 country에 따라 country_code를 부여합니다. ( Korea = KR, United States = US, Japan = JP )
그리고는 os를 택합니다. 안드로이드의 경우 카테고리가 하나로 묶어져 있지만, ios같은 경우에는 (FREE/ PAID/ GROSS)와 카테고리를 따로 택해야 합니다. 따라서, os 별로 카테고리를 택하는 과정이 다릅니다. 

3. 
create folder는 다운로드 받을 디렉토리를 설정하는 과정입니다.
입력받는 과정이 없고 직접 프로그램 내에서 고쳐야 합니다.
 

여기서 두 sequence를 각각 더블클릭 한 후에 Assign block의 directory_name 을 수정해야 합니다.
 
“C:\Users\moons\Desktop\” 이 부분을 자신이 원하는 디렉토리로 바꾸어야 합니다. 
새로 생성되는 디렉토리 이름은
안드로이드의 경우 : (Countrycode)_(OS_type)_(category)_(start_year)(start_month)_(end_year)(end_month)
애플의 경우 : (Countrycode)_(OS_type)_(iOS_type)_(category)_(start_year)(start_month)_(end_year)(end_month)

4. 
download file 단계는 받아야 하는 총 개수를 계산하고 그 만큼 카운트를 세며 download 하는 과정입니다.
4단계에 들어가기 전에 먼저 current_month와 current_year, count_year를 각각 start_month, start_year, 0으로 초기화 해줍니다.
이후엔 while ( count < number of download file) 을 통해 다운로드 합니다.

다운로드 과정은 다음과 같습니다.
오픈 브라우저 – 원하는 타입 클릭 – loading – 200 records, CSV 버튼 클릭하여 다운로드 – close browser 

오픈 브라우저 단계는 로그인 하고 각 os 타입별로 monthly를 클릭합니다.

이후에 이전에 인풋으로 받았던 값들( 카테고리, date)를 클릭하고 데이터가 로드 되길 기다립니다.
로딩이 완료됐으면 200개의 records를 누르고 CSV 버튼을 클릭하여 다운로드 합니다.

이때 크롬에서 다운로드 받으면 내 문서의 다운로드 폴더에 다운로드 됩니다. 그리고 이 다운로드 받은 폴더 내에서 가장 최근 modified된 파일 ( = 방금 받은 csv 파일 ) 이라는 점을 이용하여, 이 파일을 3번 과정에서 만든 폴더로 이동하는 process가 있습니다. 따라서, 크롬의 ’다운로드 전에 각 파일의 저장 위치 확인’ 이 반드시 해제되어야 합니다.
(위 방식의 문제점 : 간혹가다 데이터가 존재하지 않는 경우가 있었습니다. 그러면 CSV 버튼을 눌러도 아무 데이터가 받아지지 않는데 이때, 다운로드 폴더에선 가장 최근의 파일이 다운로드 받은 CSV 파일이 아니기 때문에 최종 결과로 원하지 않는 파일이 껴있을 수 있습니다.)

디렉토리로 이동시킨 파일 이름을 로그파일에 작성하고 카운트가 number_of_file 과 같아지면 프로그램은 종료합니다
