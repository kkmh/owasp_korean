============================================================================================
OTG-BUSLOGIC-002 (요청 위조 기능 테스트)
============================================================================================

|

개요
============================================================================================

Forging requests is a method that attackers use to circumvent the front end GUI application to directly submit information for back end processing. 
The goal of the attacker is to send HTTP POST/GET requests through an intercepting proxy with data values that is not supported, guarded against or expected by the applications business logic. 
Some examples of forged requests include exploiting guessable or predictable parameters or expose "hidden" features and functionality such as enabling debugging or presenting special screens or windows that are very useful during development but may leak information or bypass the business logic. 

Vulnerabilities related to the ability to forge requests is unique to each application and different from business logic data validation in that it s focus is on breaking the business logic workflow. 
Applications should have logic checks in place to prevent the system from accepting forged requests that may allow attackers the opportunity to exploit the business logic, process, or flow of the application. 
Request forgery is nothing new; the attacker uses an intercepting proxy to send HTTP POST/GET requests to the application. 
Through request forgeries attackers may be able to circumvent the business logic or process by finding, predicting and manipulating parameters to make the application think a process or task has or has not taken place. 

Also, forged requests may allow subvention of programmatic or business logic flow by invoking "hidden" features or functionality such as debugging initially used by developers and testers sometimes referred to as an "Easter egg". 
"An Easter egg is an intentional inside joke, hidden message, or feature in a work such as a computer program, movie, book, or crossword. 
According to game designer Warren Robinett, the term was coined at Atari by personnel who were alerted to the presence of a secret message which had been hidden by Robinett in his already widely distributed game, Adventure. 
The name has been said to evoke the idea of a traditional Easter egg hunt." http://en.wikipedia.org/wiki/ Easter_egg_(media) 

|

예제
============================================================================================

|

예제 1
-----------------------------------------------------------------------------------------

Suppose an e-commerce theater site allows users to select their ticket, apply a onetime 10% Senior discount on the entire sale, view the subtotal and tender the sale. If an attacker is able to see through a proxy that the application has a hidden field (of 1 or 0) used by the business logic to determine if a discount has been taken or not. The attacker is then able to submit the 1 or "no discount has been taken" value multiple times to take advantage of the same discount multiple times. 

|

예제 2
-----------------------------------------------------------------------------------------

Suppose an online video game pays out tokens for points scored for finding pirates treasure and pirates and for each level completed. These tokens can later be that can later be exchanged for prizes. Additionally each level's points have a multiplier value equal to the level. If an attacker was able to see through a proxy that the application has a hidden field used during development and testing to quickly get to the highest levels of the game they could quickly get to the highest levels and accumulate unearned points quickly. 
Also, if an attacker was able to see through a proxy that the application has a hidden field used during development and testing to enabled a log that indicated where other online players, or hidden treasure were in relation to the attacker, they would then be able to quickly go to these locations and score points. 

|


테스트 방법
============================================================================================

일반 테스트 방법
-----------------------------------------------------------------------------------------

- 프로젝트 문서를 검토하고 추측 또는 예측할 수 있거나 숨겨진 필드 함수를 찾아 테스트 공격 진행
- 어플리케이션 및 시스템에서 논리적으로 잘못된 데이터 입력 검색

|

구체적인 테스트 방법 1 
-----------------------------------------------------------------------------------------

- Using an intercepting proxy observe the HTTP POST/GET looking for some indication that values are incrementing at a regular interval or are easily guessable. 
- If it is found that some value is guessable this value may be changed and one may gain unexpected visibility. 

|

구체적인 테스트 방법 2 
-----------------------------------------------------------------------------------------

- Using an intercepting proxy observe the HTTP POST/GET looking for some indication of hidden features such as debug that can be switched on or activated. 
- If any are found try to guess and change these values to get a different application response or behavior. 

|

관련 테스트 케이스
============================================================================================

- 노출 세션 변수 테스트 (OTG-SESS-004) 
- 크로스 사이트 요청 위조 테스트 (OTG-SESS-005) 
- 계정 리스트 및 추측 가능한 사용자 테스트 (OTG-IDENT-004) 

|

도구
============================================================================================

- OWASP Zed Attack Proxy (ZAP)

|

참고 문헌 
============================================================================================

- Easter egg: http://en.wikipedia.org/wiki/Easter_egg_(media) 
- Top 10 Software Easter Eggs: http://lifehacker.com/371083/top-10-software-easter-eggs 

|

개선 방안 
============================================================================================

The application must be smart enough and designed with business logic that will prevent attackers from predicting and manipulating parameters to subvert programmatic or business logic flow, or exploiting hidden/undocumented functionality such as debugging. 

|