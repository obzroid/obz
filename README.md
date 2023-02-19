# TM SQL Comment Eclipse Plugins

1) 설치 방법 : com.roid.eclipse.tmtool_1.0.0.202302120446.jar 를 "eclipse 디렉토리\plugins"에 copy해서 넣으면 됩니다.


2) eclipse TM SQL Plugins 설명

@ 개발 환경 : eclipse 2020-06 / jdk 1.8 환경에서 개발 -- 상위 버젼도 가능할 것으로 예상


@ tmplugins_prj.zip 을 다운로드 받은 후에 eclipse 실행 >> Import > Projects from Foler or Archive 를 통하여 Archive 선택하여 zip 파일을 import
  
  
  1. roid.tmtool 이라는 eclipse plugins project를 확인
  
  
  2. plugin.xml 을 클릭하면, plugin에 대한 전반적인 사항이 나오면 중요한 내용들은 아래의 내용들입니다.
    
    . 2번째 Tab : [Dependencies] -- 플러그인에서 사용하는 의존성이 나오면 여기의 버젼들을 올려서 다시 빌드하면 상위 버젼의 이클립스용으로 업그레이드 가능
                  * 참고 : /META-INF 아래의 MANIFEST.MF 파일에서 확인 가능
    
    
    . 4번째 Tab : [Extensions] 여기에서 개발한 기능을 어디에 적용할지 정리 ==> 이 부분의 상세 내용은 [plugin.xml]에서 확인 가능
    
      * org.eclipse.ui.commands : 기본적으로 기능 수행을 위한 기본값 정의 ( plugin.xml의 <extension point="org.eclipse.ui.commands"> ~ </extension> 내용 참조
      
      * org.eclipse.ui.handlers : 실체적으로 실행될 클래스 매핑, 기능이 실행될 스코프 등을 정의
      
            - 현재 이 기능은 Java File Editing 상태일때 기능
            
            > com.roid.eclipse.tmtool.commt.SqlCmmtHandler.java : SQL_START가 포함된 라인 부터 SQL_END가 나올때까지 주석 처리 하는 기능
            > com.roid.eclipse.tmtool.commt.SqlDeCmmtHandler.java : SQL_START가 포함된 라인 부터 SQL_END가 나올때까지 주석 제거 하는 기능
      
      * org.eclipse.ui.menus : 기능을 표시할 메뉴 위치 설정 등
            - 현재 toolbar에 /icons 아래에 있는 아이콘으로 실행 가능하도록 추가 하였고, 상단의 메뉴에 [TM Tools]라는 메뉴 추가, 그외 Source 메뉴에도 나오도록 세팅함
            
    
3) 소스 설명  
  - Activator.java : 이클립스 플러그인 샘플 프로젝트 생성시 기본 형태
  
  - com.roid.eclipse.tmtool.commt
      SqlCmmtHandler.java
      SqlDeCmmtHandler.java
      
      execute() method : 
          . if (JAVA_EDITOR_ID.equals(activePartId)) 아래 내용 부분들에 실구현 부분 처리
          . SQL_START ~ SQL_END 가 포함된 라인 주석 처리 또는 주석 해제 처리 구현부
      
  - 그외     
    SqlCmmtActionDelegate.java
    SqlDeCmmtActionDelegate.java
    
    위의 소스는 현재 사용되지 않음. ActionSet 구현할려 하였으나, 특별한 동작을 하지 않아서 제외처리
    

4 ) Build 방법
  . 프로젝트 roid.tmtool 선택하여 > Run As > Eclipse Application 선택 
  . 실행 이후 상단에 추가한 플러그인들 확인

  아래와 같은 예제가 정상적으로 주석 처리 및 해제 되는지 확인

//	@SQL_START <br />
//		ssss <br />
//		ddddd <br />
//	@SQL_END <br />
	
fsdfsdfs
fdsfsd
	
fdsfsdf
	
fsdfsd

//	@PSQL_START <br />
//		ssss <br />
//		ddddd <br />
//	@PSQL_END <br />
  
  
  
5)  플러그인 jar 생성 
  . Export > Plug-in Development > Deployable features 선택
  . 디렉토리 선택 후 Finish
