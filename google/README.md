# google-api
google-api 사용법

### Environment
* Google Cloud Platform Console
  * 새 프로젝트 생성
  * Google Drive API 시작
  * Google Sheets API 시작
  * Google API 계정 및 Key 생성

### Google Spreadsheet API
* Install
  * ```
    $ pip install gspread oauth2client
    ```

* Example
  * Load from URL
    ```
    from oauth2client.service_account import ServiceAccountCredential
    import gspread

    scope = ['https://spreadsheets.google.com/feeds', 'https://www.googleapis.com/auth/drive']
    credentials = ServiceAccountCredentials.from_json_keyfile_name('GOOGLE_KEY.json', scope)

    gc = gspread.authorize(credentials)
    doc = gc.open_by_url('GOOGLE_SHEET_URL') # URL은 Google Cloud Platform API 계정과 공유되어 있어야 함
    
    worksheet = doc.worksheet('SHEET_NAME')
    ```

  * Get value
    ```
    worksheet.range('A1:Z10')     # A1부터 Z10까지 데이터를 리스트로 가져옴 (순서는 A1, A2, A3, ... Z9, Z10)
    worksheet.row_values(n)       # n행의 데이터를 리스트로 가져옴 (0번째 데이터의 값은 list[0].value)
    worksheet.col_values(n)       # n열의 데이터를 리스트로 가져옴
    worksheet.acell('A1').value   # 1행 1열의 데이터의 값을 가져옴
    ```
    