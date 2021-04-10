# Swift 문법
> 2018.02.21 업데이트    

## UITableView
* 리스트의 형태로 정보를 보여주는 View

### Plain Table Views
* 기본적인 TableView  
* 여러개의 Section을 가질수 있다.   
* 한 Section에는 여러개의 Row를 포함하고 있으며, 한개의 row를 cell이라 부른다.
* 각각의 Section에는 Section을 표시하는 header, Footer title을 사용할수 있다.  
* Section을 빠르게 검색할수 있는 네비게이터 바를 index list 라고 부른다.

### Grouped Table Views
* 각 Section을 Group의 형태로 나타내는 테이블 뷰.  
* 데이터의 디테일한 정보를 표현할때 많이 사용된다.

### DataSource 
* 프로토콜을 사용하여 테이블뷰에서 보여줄 데이터를 관리할 대리인의 역할을 정의해둔 것
* 역할
    - @requires