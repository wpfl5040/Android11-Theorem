# Android 11 Meetups 정리

## 안드로이드 흐름
 - Android 9 
    > 백그라운드에서 마이크, 카메라등 센서 정보 사용제한 
    > 새로운 CALL_LOG 권한 그룹 추가
    > WI-FI 스캔 기능은 정밀한 위치 권한을 요구
 - Android 10
    > 개인정보 보호 메뉴가 최상단 메뉴로 변경
    > 백그라운드에서 위치 정보 접근을 위한 새로운 백그라운드 위치 권한
    > 백그라운드에서 액티비티 실행 금지
    > 재설정 불가능한 디바이스 식별자 접근 금지
 - Android 11
   > 1. 권한 자동 재설정
   > 2. 패키지 공개 상태 
   > 3. 일회성 권한
   > 4. 백그라운드 위치 액세스
   > 5. 범위 지정 저장소 적용
   > 6. 새로운 포그라운드 서비스 유형
   > 7. 데이터 액세스 분석
  
  ## Android 11 바뀐 점
  1. 권한 자동 재설정
	    >  타깃 SDK가 Android 11 이상인 앱의 경우, 사용자가 사용하지 않는 앱의 런타임 요청 권한이 자동으로 초기화 됨
		> 타깃 SDK 버전이 Android 11 미만인 경우에도 사용자가 명시적으로 해당 기능 적용 가능 
  2. 패키지 공개 상태
		> 타깃 SDK가 Android 11 이상인 앱의 경우, 디바이스에 설치된 다른 앱 목록을 알 수 없음
		> 특정 패키지 설치 여부를 꼭 확인할 필요가 있는 경우, 앱 매니페스트에 미리 선언
		
		>  **QUERY_ALL_PACKAGES **
		> - 설치된 모든 앱 목록을 확인할 수 있는 권한
		> - Google Play 정책으로 사용이 제한 됨

	3. 일회성 권한
		> 타깃 SDK 버전과 관계없이 카메라, 마이크, 위치 권한에 적용
		> 허용, 거부  ----->  앱 사용 중에만 허용, 이번만 허용, 거부
		> 백그라운드에 진입 후 일정 시간이 지나면 권한 다시 회수

	4. 백그라운드 위치 액세스
		> 타깃 SDK 버전과 관계없이 적용
		> 위치 권한 요청 시, 항상 허용 옵션이 제외 됨
		> 사용자는 시스템 설정 화면에서 항상 허용 옵션을 선택할 수 있음
		> 사용자가 명시적으로 백그라운드 위치 권한을 허용 해 줘야 사용 가능
	
	5. 범위 지정 저장소
		> 타깃 SDK가 Android 11 이상인 앱의 경우 반드시 적용
		> 별도 권한 요청 없이
		>  - 액별 디렉토리에 자유롭게 읽고 쓰기 가능
		>  - 공유 저장소에 파일 생성 가능
		>  - 자신이 생성한 파일은 읽기 및 쓰기 가능
		> 다른 앱이 생성한 미디어 파일은 필요한 권한 획득 후 사용 가능

	6. 카메라, 마이크 포그라운드 서비스 타입
		> 타깃 SDK가 Android 11 이상인 앱의 경우 적용
		> 매니페스트 상에 올바른 타입을 선언하지 않은 경우 포그라운드 서비스에서 카메라, 마이크 접근 금지
		> 
		> ````
		> 	<manifest>
		>		<service ...
		>			android:foregroundServiceType="camera|microphone" />
		>  	</manifest>
	    > ````

	7. 데이터 액세스 분석
		> 권한이 필요한 기능을 수행하는 코드를 확인
		> 앱에 포함된 SDK에서 사용하는 경우도 확인 가능
		> 런타임 권한이 필요한 API 호출 시, 콜백이 호출 됨
		
  ## 사용자를 위한 기능
  1. 대화 공간
	  > 알림 영역 최상단에 별도의 대화 공간이 추가 됨
	  > MessagingStyle이 적용된 알림을 해당 곤간에 표시
	  > **버블** 및 **중요 대화 표시** 등 대화와 관련된 추가 기능을 제공
	  > - **버블**
	  >    - 안드로이드 10 버전에서는 개발자 미리보기 형태로 지원
	  >    - 앱이 버블 기능을 지원하는 경우, 사용자는 원하는 대화를 버블 형식으로 표시 가능
	  >    - 버블을 탭 하면 등록된 액티비티가 화면 가장 전면에 표시
	  
      > - **중요 대화** 
      >    - 대화 알림을 길게 누른 후 대화 중요도 설정 가능
      >    - 중요 대화는 방해 금지 를 무시할 수 있음
      >    -  중요 대화는 AOD 상에 아이콘 형태로 표시
	      
   2. 새로운 미디어 컨드롤 UI
	   > Android 11 베타 2 버전부터 기본 지원
	   > MediaSession을 포함한 MediaStyle 알림 사용 시, 자동으로 새로운 UI 적용
	   > 빠른 설정 패널 상에 위치, 쉽게 미디어 컨트롤 가능
	   > 미디어 출력 장치를 손쉽게 변경 가능 
	   > MediaBrowserService가 요구 사항을 만족하면, 디바이스 재부팅 후에도 미디어 컨트롤 UI가 유지 됨

	3. 외부 장치 컨트롤
	   > 스마트 조명 등, 외부 장치를 빠르게 확인하고 컨트롤 할 수 있는 UI를 제공
	   > 개발자는 ControlsProviderService를 구현
	   > 사용자는 여러 ControlsProvider 중 하나를 선택 가능
	   >  미리 정해진 템플릿을 활용 UI를 표현 - 정적 버튼, 토글, 범위, 토글 + 범위, 온도
	   
	 4. 키보드 전환 애니메이션
	    > 앱에서 키보드 전환 애니메이션을 확인하고 앱의 동작을 변경 할 수 있는 새로운 API 제공
	    > 사용자가 원하는 대로 키보드 전환 애니메이션을 변경 할 수 있는 새로운 API 제공
	    > ```
	    > **System Window 애니메이션에 따른 콜백**
	    >  v.onApplyWindowInsetsListener = ...
	    >  v.windowInsetsAnimationCallback = object {
	    >		fun onProgress(insets: WindowInsets) { 
	    >				v.setY(calculateYFor(insets))
	    >		}
	    >	}
	    >```
	    >```
	    > **System Window 애니메이션 조절**
	    > v.windowInsetsControler
	    >		.controlInputMethodAnimation() { anim -> 
	    >				anim.setInsetsAndAlpha(calcInsets(), ... )
	    >		}
	    >```

	4. 키보드와 통합된 자동 완성 제안
		> Autofill Framework
		> Jetpack Autofill
		>   - Autofill에서 원하는 데이터를 키보드에 제안할 수 있는 새로운 API 추가
		>   - Autofill에서 가져온 데이터를 키보드에 표시할 수 있는 새로운 API 추가
	 
	 5. 이미지 복사 및 붙여넣기
		 > 크롬 브라우저에서 이미지 복사 기능 지원
		 > G-Board의 키보드 제안 팁에서 이미지 클립보드 표시
		 > Jetpack RichContentReceiverCompat : 쉽게 이미지 붙여넣기 기능을 구현할 수 있는 라이브러리
		 
  ## 새로운 하드웨어 (폴더블)
1. 화면 정보 확인하기
	> Hinge 센서 타입
	>> Android 11 에서 새롭게 추가
	>> 디바이스가 접힌 각도 확인 가능
	>> 디바이스 마다 개별 처리가 필요
	
	>Jetpack Windows Manager
	>> Android 11 이전 버전에서도 사용 가능
	>> 윈도우 타입, 영역, 상태 정보를 확인 가능
	>> 디바이스의 자세 정보를 확인 가능

2. 다양한 디바이스 테스트
	
  ## 5G를 위한 기능
  1. 무제한 네트워크 확인
	  > 통신사와 협력을 통해 무제한 네트워크 여부를 보다 정확하게 파악
  2. 네트워크 속도 예측

> Blockquote
	  > 예측된 속도의 정확성이 향상 됨
  3. 5G 연결 여부 확인
		> PhoneStateListener#onDisplayInfoChanged


# 참고 자료
  - https://developer.android.com/preview
  - https://developersonair.withgoogle.com/events/a11meetup-korea
