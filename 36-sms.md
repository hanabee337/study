# COOLSMS API를 이용한 SMS(단문) 보내기

##  1. 초기 설정
- 가상환경 설정, 필요 패키지 설치, 
- ```.conf 폴더``` 생성 및 ```setting_local.json``` 파일 생성
- ```setting_local.json``` 파일에는 하기와 같은 내용들이 관리되고 있다.

```python
{
  "django": {
    	"secret_key": "settings.py에 있는 SECRET_KEY"
  },

  "sms": {
    	"username": "coolsms 아이디",
    	"password": "비밀번호",
    	"sender_num": "보내는 사람의 전화번호",
    	"API_KEY": "CoolSMS 환경설정에 있음",
    	"API_SECRET": "CoolSMS 환경설정에 있음"
  }
}
```

## 2. CoolSMS API 사용하기
- 하기 사이트에 나와있는 Step 1 ~ 4까지 따라하기
[http://www.coolsms.co.kr/Python_SDK_Start_here](http://www.coolsms.co.kr/Python_SDK_Start_here)  

	1. Step 1 : 
	```
	pip install coolsms_python_sdk
	```

	2. Step 2 : 회원 가입
		- 강사님 id/pw로 로그인 : .conf/settings_local.json에서 관리
	
	3. Step 3 : API KEY 생성
		- [환경설정](https://www.coolsms.co.kr/index.php?mid=service_setup&act=dispSmsconfigCredentials) 페이지로 가서 2016-10-18자 API Key와 API Secret 번호 사용하면 됨. 이것도 .conf/settings_local.json에서 관리

- 참고사항에 보면, 발신번호를 사전등록해야 된다고 함. 강사님 손전화번호로 등록되어 있음.

- Step 4. 문자 보내기의 [Example](http://www.coolsms.co.kr/Python_SDK_Example) 에 잘 나와있다고 함
- Example의 [Message](http://www.coolsms.co.kr/Python_SDK_EXAMPLE_Message) 클릭

- 상기 내용을 토대로 sms_test/sms.py에서 동작 구현해보기
- 구현된 코드는 아래와 같다.
```python
import json
import os
import sys

from sdk.api.message import Message
from sdk.exceptions import CoolsmsException

ROOT_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
print(ROOT_DIR)

CONF_DIR = os.path.join(ROOT_DIR, '.conf')

config_content = open(os.path.join(CONF_DIR, 'settings_local.json')).read()
print(config_content)

config = json.loads(config_content)
print(config)

if __name__ == "__main__":
    # set api key, api secret
    api_key = config['sms']['API_KEY']
    api_secret = config['sms']['API_SECRET']

    # 4 params are mandatory, must be filled.
    params = dict()
    params['type'] = 'sms'  # Message type(sms, lms, mms, ata)
    params['to'] = config['sms']['receiver_num']  # Recipients Phone Number
    params['from'] = config['sms']['sender_num']  # Sender number
    params['text'] = 'Where are you?'  # Message to send

    cool = Message(api_key, api_secret)

    try:
        response = cool.send(params)
        print("Success Count : %s" % response['success_count'])
        print("Error Count : %s" % response['error_count'])
        print("Group ID :%s" % response['group_id'])

        if "error_list" in response:
            print("Error List : %s" % response['error_list'])

    except CoolsmsException as e:
        print("Error Code : %s" % e.code)
        print("Error Message : %s" % e.msg)

    sys.exit()
```
- 전화번호 validation 코드 추가(sms/forms.py)
```python
class SMSForm(forms.Form):
    # recipient_numbers = forms.CharField(max_length=500)
    recipient_numbers = forms.CharField(
        max_length=500,
        widget=forms.TextInput(
            attrs={
                'size': '100',
            }
        )
    )
    content = forms.CharField(widget=forms.Textarea())

    def clean_recipient_numbers(self):
        cleaned_numbers = []
        p = re.compile(r'^0\d{9}\d?$')
        number_string = self.cleaned_data['recipient_numbers']
        print('number_string: {}'.format(number_string))
        numbers = number_string.replace('-', '').replace(' ', '').split(',')
        print('numbers: {}'.format(numbers))
        for number in numbers:
            if re.match(p, number):
                cleaned_numbers.append(number)
            else:
                raise ValidationError('Invalid phone number format: {}'.format(number))

        return cleaned_numbers
```
- 위의 코드 실행 결과 아래와 같이, 잘 걸러낸 것을 확인할 수 있다.
```python
>>> c = '010-1234-5678, 01012345678, 01023412, 293849323232, 02394090930'
>>> import re
>>> p = re.compile(r'^0\d{9}\d?$')
>>> p
re.compile('^0\\d{9}\\d?$')
>>> numbers = c.replace('-','').replace(' ','').split(',')
>>> numbers
['01012345678', '01012345678', '01023412', '293849323232', '02394090930']
>>> 
>>> for number in numbers:
...     print(re.match(p, number))
... 
<_sre.SRE_Match object; span=(0, 11), match='01012345678'>
<_sre.SRE_Match object; span=(0, 11), match='01012345678'>
None
None
<_sre.SRE_Match object; span=(0, 11), match='02394090930'>
```