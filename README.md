# JpaAdvance_exampleCode
## Entity 연관 관계 실습

  1. 1 대 1 관계    
  ### 단방향    
  - 외래 키 주인만이 외래 키를 등록, 수정, 삭제할 수 있으며, 주인이 아닌 쪽은 오직 외래 키를 읽기만 가능합니다.    
  ### 양방향    
  - mappedBy의 속성값은 외래 키의 주인인 상대 Entity의 필드명을 의미합니다.   
 
  2. N 대 1 관계
  ### 단방향   
  - Entity가 N의 관계로 외래 키의 주인    
  ### 양방향    
  - 음식 Entity가 N의 관계로 외래 키의 주인      
  - 양방향 참조를 위해 고객 Entity에서 Java 컬렉션을 사용하여 음식 Entity 참조        
  ```
  고객
  @OneToMany(mappedBy = "user")
    private List<Food> foodList = new ArrayList<>();
  ```


  3. 1 대 N 관계     
  ### 단방향
  - 외래 키를 관리하는 주인은 음식 Entity이지만 실제 외래 키는 고객 Entity가 가지고 있습니다.    
  ```
  음식
  @OneToMany
  @JoinColumn(name = "food_id") // users 테이블에 food_id 컬럼
  private List<User> userList = new ArrayList<>();
  ```
    
  ### 양방향     
  - 1 대 N 관계에서는 일반적으로 양방향 관계가 존재하지 않습니다.    

  4. N 대 M 관계    
  - N : M 관계를 풀어내기 위해 중간 테이블(orders)을 생성하여 사용합니다.        

  5. 지연 로딩        
  - `LAZY`는 `지연 로딩`으로 필요한 시점에 정보를 가져옵니다.      
  - `EAGER`는 `즉시 로딩`으로 이름의 뜻처럼 조회할 때 연관된 모든 Entity의 정보를 즉시 가져옵니다.      

  6. 영속성 전이        
  - 영속 상태의 Entity에서 수행되는 작업들이 연관된 Entity까지 전파되는 상황을 뜻합니다.    
  - 영속성 전이를 적용하여 해당 Entity를 저장할 때 연관된 Entity까지 자동으로 저장하기 위해서는 자동으로 저장하려고 하는 연관된 Entity에 추가한 연관관계 애너테이션에 CASCADE의 PERSIST 옵션을 설정하면됩니다.    

  7. 고아 Entity 삭제        
  -  CASCADE의 REMOVE 옵션을 적용하면 해당 Entity 객체를 삭제 했을 때 연관된 Entity 객체들을 자동으로 삭제할 수 있었습니다.    
  -  orphanRemoval 옵션도 REMOVE 옵션과 마찬가지로 해당 Entity 즉, Robbie Entity 객체를 삭제하면 연관된 음식 Entity들이 자동으로 삭제됩니다.
