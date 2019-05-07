# SOFTWARE ENGINEERING IN JAVA

## Session 30 (16/04/2019)

- Reviewing sprint project (issue) tasks and solving problems and feedback
- Reviewing main project tasks and planning next Sprint

## Notes

#### Reviewing sprint project (issue) tasks and solving problems and feedback

removed markers of test is to run application in controller

```
@RunWith(SpringRunner.class)
@SpringBootTest
```

With this I have to declare ENV but as Im using unit test I don't need this

integration Im loading all Spring thing



unit test just loading junit (less than 1 sec)

Integration 1 sec





create variable with accountResponse,getData.get

import assert



reformat code





service 

rename name of variable



```
private AccountService target = new AccountService();
```



```
    accountList.getData().add(account);

}
return null;
```



```
Assert.assertNotNull(accounts);
```



```
account.setAccount("user_" + i);
account.setFullName("Test User " + i);
accountList.getData().add(null);
```





```
for (Account account : accounts.getData()) {
    Assert.assertNotNull(account);
```



import statuc for assertNotNull

deleting this 



```
@Test
public void inMemoryAccountsNotNull() {
    ListAccountsResponse accounts = target.listAccounts();
    assertNotNull(accounts);

}
```



becasue this was alreadu done in 



```
assertNotNull(accounts);
```





```
public class WalletApplicationServiceTests {
...
private AccountService target = new AccountService();
....
```



```
ListAccountsResponse accounts = target.listAccounts();
```



```
public class WalletApplicationServiceTests {

    @Test
    public void returnsValidData() {
        ListAccountsResponse accounts = new AccountService().listAccounts();
```



build.gradle

```
runtimeOnly 'mysql:mysql-connector-java'
```



this says taht we're going to use mysql implementation



renaming tests



```
@Test
public void whenNotDataInDBReturnEmptyJSON() {
    Mockito.when(mockRepo.findAll()).thenReturn(new ArrayList<>());

}
```



check return nan emprty aray when no data in db



```
@Test
public void whenNotDataInDBReturnEmptyJSON() {
    Mockito.when(mockRepo.findAll()).thenReturn(new ArrayList<>());
    ListAccountsResponse response = target.listAccounts();
    Assert.assertEquals(0, response.getData().size());

}
```



java.lang.AssertionError: 
Expected :0
Actual   :10





So we delete this 



```
return accountList;
```



for this



```
return new ListAccountsResponse();
```



in order to retrieve an empty list and test pass





Now I delete the old test testing the hardcoded data



```
@Test
public void returnsValidData() {

    ListAccountsResponse accounts = target.listAccounts();
    assertNotNull(accounts);
    Assert.assertEquals(10, accounts.getData().size());
    for (Account account : accounts.getData()) {
        assertNotNull(account);
        assertNotNull(account.getId());
        assertNotNull(account.getAccount());
        assertNotNull(account.getFullName());
    }

}
```





borro  



```
final ListAccountsResponse accountList = new ListAccountsResponse();
for (int i = 0; i < 10; i++) {
    final Account account = new Account();
    account.setId(Long.valueOf(i));
    account.setAccount("user_" + i);
    account.setFullName("Test User " + i);
    accountList.getData().add(account);
```



de



```
ListAccountsResponse listAccounts() {

    return new ListAccountsResponse();

}
```



Para hacer Long account.setId(1L);



works also with lowercase l but better with L 



aqu ino se usa set porque get ya me trae los datos si se usa data se reasigna el array 



```
class ListAccountsResponse {
    private List<Account> data = new ArrayList<>();

    public List<Account> getData() {
        return data;
    }

    public void setData(List<Account> data) {
        this.data = data;
    }


}
```



```
List<Account> list = new ArrayList<>();
list.add(makeAccount());
when(mockRepo.findAll()).thenReturn(list);
```



to



 when(mockRepo.findAll()).thenReturn(Arrays.asList(makeAccount()));



we import statically



 when(mockRepo.findAll()).thenReturn(asList(makeAccount()));





refacot r





```
Iterable<Account> accounts = accountRepository.findAll();
ListAccountsResponse accountsResponse = new ListAccountsResponse();
for (Account account : accounts) {
    accountsResponse.getData().add(account);
}
```



to 



```
ListAccountsResponse accountsResponse = new ListAccountsResponse();
for (Account account : accountRepository.findAll()) {
    accountsResponse.getData().add(account);
}
```



for each test I define with mockito what is going to return





As I create a test to test 5 elements not need the one test 1



```
@Test
public void whenThereIsOneAccountInDBReturnOneAccountJSON() {
    when(mockRepo.findAll()).thenReturn(asList(makeAccount(1L)));
    ListAccountsResponse response = target.listAccounts();
    assertEquals(1, response.getData().size());
    Account actual = response.getData().get(0);
    assertEquals(Long.valueOf(1), actual.getId());
    assertEquals("account_1", actual.getAccount());
    assertEquals("Account number 1", actual.getFullName());

}
```

```
@Test
public void whenThereIsFiveAccountInDBReturnFiveAccountJSON() {
    when(mockRepo.findAll()).thenReturn(asList(
            makeAccount(1L),
            makeAccount(2L),
            makeAccount(3L),
            makeAccount(4L),
            makeAccount(5L)
            ));
    ListAccountsResponse response = target.listAccounts();
    assertEquals(5, response.getData().size());
    for (int i = 0; i < response.getData().size(); i++) {
        Account actual = response.getData().get(i);
        assertEquals(Long.valueOf(i+1), actual.getId());
        assertEquals("account_" + (i+1), actual.getAccount());
        assertEquals("Account number " + (i+1), actual.getFullName());
    }

}
```



estuvimos haciendo TDD el error y luego verde y luego refactor quitando repeticiones poniendo variables inlie, sacando como varaibles  valores repetidos. 



con mockito se prueban todos los metodos sin necesidad de implementar nada en el lado del servidor, uno define la respuesta que quiere dar.

se usa en test unitarios para imitar las clases de las que depende lo que se prueba



se hcieiron varios tests para el servicio y se arreglaron los del controlador



en el servicio se pueden hacer mas tests pero el que esta listAccounts ya esta en el punto que deberia estar.



### Homework









- To do the [](https://github.com/javarb/wallet/issues/) tasks as defined in the [project issue board](https://github.com/javarb/wallet/projects/)



### Resources

[1]: http:// 
[2]: https:
