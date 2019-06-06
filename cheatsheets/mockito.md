# Mockito cheatsheet

## Annotations basiques

Sur la classe :

- @RunWith(SpringJUnit4ClassRunner.class)
- @SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)
- @ActiveProfiles({"test"})
- @TestPropertySource(locations = "classpath:application-test.properties")

Pour injecter les mocks sur le service à tester :

- @InjectMocks

Pour définir des mocks à injecter :

- @Mock

## Gestion des configurations

Si un Bean utilise des properties @Value -> utiliser ReflectionTestUtils.setField (méthode la plus simple)

## Power Mock

Attention à son utilisation, utile par exemple pour Mocker des appels statiques et classes final.

- @PrepareForTest(Factory.class)

Définir une méthode d'init (@Before) avec :

- MockitoAnnotations.initMocks(this)
- PowerMockito.mockStatic(Factory.class)
