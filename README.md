# spring-boot-style-guide

## Table of Contents

* [Dependency Injection](#dependency-injection)

* [Mockito Testing](#mockito-testing)

## Dependency Injection
* <a name="dependency-injection"></a>
  Prefer using constructor injection over field injection. Constructor injection clearly specifies the dependencies, and no autowired bean will be forgotten in writing the tests.
<sup>[[link](#dependency-injection)]</sup>

## Mockito Testing

* <a name="mockito-testing"></a>
  Prefer using annotations like @Mock, @Spy, @InjectMocks and @Captor over old way without annotations.
<sup>[[link](#mockito-testing)]</sup>

* <a name="inject-real-objects"></a>
  Inject real objects into private @Autowired fields. Mockito will consider all fields having @Mock or @Spy annotation as potential candidates to be injected into the instance annotated with @InjectMocks annotation. 
  In the following case 'clientProperties' instance will get injected into the 'clientAdaptor', and 'clientAdaptor' will get injected into the 'clientServiceImp'.
<sup>[[link](#inject-real-objects)]</sup>
```Java
@RunWith(MockitoJUnitRunner.class)
public class DemoTest {
    @Mock
    private ClientProperties clientProperties;

    @Spy
    @InjectMocks
    private ClientAdaptor clientAdaptor = new ClientAdaptor();

    // clientServiceImp has a clientAdaptor, while the clientAdaptor has a clientProperties
    @InjectMocks
    private ClientServiceImp clientServiceImp = new clientServiceImp();
}
```
