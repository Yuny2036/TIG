# Visual Studio Code <sub>VSCode</sub>
------
## 서론
Visual Studio Code<sub>이하 VSCode 또는 VSC</sub>를 사용하면서 겪었던 불편사항의 대응이나 유의사항 및 괜찮은 정보 등을 기록하고자 해당 문서를 개설하게 되었다. 각종 기록이 무분별하고 순서없이 기록될 수 있기 때문에 ***있을 법한*** 키워드를 `Ctrl + F` 를 통해 검색하는 것을 권장하는 바이다.
------
------
## VSC 작업내용 자동 저장 설정
```json
{
  "files.autoSave": "afterDelay",
  "files.autoSaveDelay": 1000
}
```
해당 설정은 VSCode 의 `settings > 'auto'` 를 검색해서도 쉽게 찾을 수 있다. 단, 저장 딜레이는 따로 탭이 없으므로 `settings.json` 을 수정해야 할 것이다.