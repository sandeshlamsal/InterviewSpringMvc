# InterviewSpringMvc
why sprig popular ?
dependeny injection or Inversion of Control, can use classes that you want just by autowiring
don't have to use the new keyword, but with some <xml> file or annotation based we can use the required class

eg: if any clientBusiness depends upon client and product classes
then in clientBusiness class we can just
call the dependent object as

@Service
public class ClientBOImpl implements ClientBO{
@AutoWired
clientDO client;

@AutoWired
ProdutDO product;
}


versions
-------
spring 2.5=annotation
spring 3.0= java 5 new (genrics)
spring 4= java 8 (latest) lambda.. min 6 is required, @RestController,  (servlet 3.0 is used)

AutoWiring
----------
auto finding of required bean depedencies
@service  and @Component should be used
