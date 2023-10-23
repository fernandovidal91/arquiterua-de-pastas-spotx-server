# Domain Layer

A camada de "Domain" desempenha um papel fundamental em nossa aplicação, seguindo os princípios da arquitetura limpa. Ela é o centro das regras de negócio e lógica central do sistema. Nesta camada, organizamos nossos contratos de classes, modelos de entidades e regras de negócio com precisão.

## Estrutura de Pastas

```
domain/
    ├── contracts/
    │   ├── gateways/
    │   ├── protocols/
    │   ├── repositories/
    │   └── use-cases/
    ├── entities/
    │   ├── errors/
    │   └── model-mocks/
    ├── models/
    └── use-cases/
```

## Pasta "contracts"

A pasta "contracts" na camada de "Domain" desempenha um papel fundamental em nossa aplicação, garantindo a organização e a clareza dos contratos de muitas classes essenciais do sistema. Estes contratos definem interfaces, estabelecem responsabilidades e ajudam a manter uma estrutura sólida e flexível em nosso código.

Dentro desta pasta, encontramos contratos para uma variedade de componentes, incluindo repositórios, use-cases e gateways. Eles descrevem como esses componentes devem interagir, especificando as entradas, saídas. Essa abordagem é crucial para promover a separação de preocupações, facilitar a manutenção e permitir a adaptação da aplicação a mudanças futuras.

A pasta "contracts" serve como um alicerce sólido em nossa camada de "Domain", garantindo que todos os componentes da aplicação estejam alinhados com as interfaces definidas e permitindo uma maior flexibilidade e testabilidade em nosso código.

### Padrões para Contratos de "Use-Cases"

Dentro da pasta "contracts", os contratos dos "use-cases" desempenham um papel crítico ao definir as interfaces para as operações essenciais de nossa aplicação. Para garantir a consistência e a clareza desses contratos, seguimos um conjunto de padrões bem definidos:

1. **Nome do Arquivo com a Ação:** O nome do arquivo que contém o contrato do use-case deve refletir a ação a ser executada, como "create", "find", "list" e assim por diante, seguido de "use-case."

2. **Nomeação como Interface:** Ao criar um contrato de "use-case", utilizamos a palavra-chave "interface" para defini-lo, indicando claramente que se trata de uma interface que estabelece um contrato de implementação.

3. **Padrão de Nomenclatura:** O nome de um contrato de "use-case" segue um padrão claro. Ele começa com a letra 'I' seguida da ação que será executada, como "Create", "List", "Find", "Update" e assim por diante. O nome do "use-case" termina com "UseCase", refletindo sua função principal na aplicação.

4. **Método "execute":** Cada contrato de "use-case" deve conter um único método público chamado "execute." Este método é o ponto de entrada para a execução da operação do "use-case" e define como a ação deve ser realizada.

5. **Parâmetros Nomeados como 'params':** Se o método "execute" requer parâmetros, o nome da variável que armazena esses parâmetros deve ser "params", proporcionando uma convenção uniforme e legibilidade.

6. **Utilização da Tag "namespace":** Para definir os tipos de entrada e saída do método "execute", utilizamos a tag "namespace" com o mesmo nome da interface do "use-case." Isso cria um espaço de nomes específico para os tipos relacionados a esse "use-case."

7. **Definição dos Tipos de Entrada e Saída:** Dentro do espaço de nomes criado com a tag "namespace", utilizamos a tag "type" para definir os tipos de entrada e saída do "use-case." Esses tipos são nomeados como "Input" e "Output", proporcionando clareza e uniformidade. Em situações especiais, quando necessário, a tag "interface" pode ser usada para criar tipos personalizados de entrada e saída.

Seguindo esses padrões, garantimos que nossos contratos de "use-cases" sejam consistentes e de fácil compreensão, permitindo uma implementação eficaz das regras de negócio em nossa aplicação.

Exemplo:

```typescript
import { UserModel } from '@/domain/models';
import { UsersRoleEnum } from '@/domain/shared/concerns/EnumTypes';

export interface ICreateUserUseCase {
  execute(params: ICreateUserUseCase.Input): Promise<ICreateUserUseCase.Output>;
}

export namespace ICreateUserUseCase {
  export type Input = {
    name: string;
    email: string;
    phone: string;
    omieCode?: string;
    password: string;
    passwordConfirmation?: string;
    role: UsersRoleEnum;
  };

  export type Output = UserModel | null;
}
```

### Padrões para Contratos de Repositórios

Dentro da pasta "contracts", os contratos de repositórios desempenham um papel fundamental ao definir as interfaces para operações de leitura e gravação em nossa aplicação. Para garantir a consistência e a clareza desses contratos, seguimos um conjunto de padrões bem definidos:

1. **Nome do Arquivo com a Ação:** O nome do arquivo que contém o contrato do repositório deve refletir a ação a ser executada, como "create", "find", "list" e assim por diante, seguido de "repository."

2. **Nomeação como Interface:** Ao criar um contrato de repositório, utilizamos a palavra-chave "interface" para defini-lo, indicando claramente que se trata de uma interface que estabelece um contrato de implementação.

3. **Padrão de Nomenclatura:** O nome do contrato do repositório segue um padrão consistente. Ele começa com a letra 'I' seguida da ação a ser executada, como "Create", "List", "Find", "Update" e assim por diante. O nome do repositório termina com "Repository", refletindo sua função principal na aplicação.

4. **Interface e Namespace Únicos:** Cada arquivo de contrato de repositório deve conter apenas uma interface e um namespace. Dentro da interface, deve haver somente um método. Se houver necessidade de criar mais métodos de repositório, é recomendável criar um novo arquivo específico para cada método.

5. **Parâmetros Nomeados como 'params':** Se o método do repositório requer parâmetros, o nome da variável que armazena esses parâmetros deve ser "params", proporcionando uma convenção uniforme e legibilidade.

6. **Utilização da Tag "namespace":** Para definir os tipos de entrada e saída do método, utilizamos a tag "namespace" com o mesmo nome da interface do repositório. Isso cria um espaço de nomes específico para os tipos relacionados a esse repositório.

7. **Definição dos Tipos de Entrada e Saída:** Dentro do espaço de nomes criado com a tag "namespace", utilizamos a tag "type" para definir os tipos de entrada e saída do repositório. Esses tipos são nomeados como "Input" e "Output", proporcionando clareza e uniformidade. Em situações especiais, quando necessário, a tag "interface" pode ser usada para criar tipos personalizados de entrada e saída.

8. **Evitar Reutilização de Tipos:** É importante evitar a reutilização de tipos, mesmo que sejam idênticos. Por exemplo, se a entrada de um "use-case" for exatamente a mesma que a de um repositório, é recomendável criar um novo tipo em vez de reutilizar um existente. Isso ajuda a manter a separação de preocupações e a evitar problemas potenciais no futuro.

Seguindo esses padrões, garantimos que nossos contratos de repositórios sejam consistentes e de fácil compreensão, permitindo uma implementação eficaz das operações de leitura e gravação em nossa aplicação.

Exemplo:

```typescript
import { UserModel } from '@/domain/models';
import { UsersRoleEnum } from '@/domain/shared/concerns/EnumTypes';

export interface ICreateUserRepository {
  create(
    params: ICreateUserRepository.Input,
  ): Promise<ICreateUserRepository.Output>;
}

export namespace ICreateUserRepository {
  export type Input = {
    name: string;
    email: string;
    phone: string;
    omieCode?: string;
    password: string;
    passwordConfirmation?: string;
    role: UsersRoleEnum;
  };
  export type Output = UserModel | null;
}
```

## Pasta "entities"

Dentro da pasta "entities" na camada de "Domain", encontramos duas subpastas essenciais que desempenham funções cruciais em nossa aplicação.

#### Subpasta "errors"

A subpasta "errors" abriga uma variedade de tipos de exceções que são lançados em nosso sistema para lidar com situações específicas. Esses erros, como "unauthorized-error", "not-found-error", "server-error" e outros, desempenham um papel importante na sinalização de condições excepcionais durante a execução da aplicação. Eles permitem que nossa aplicação lide com casos de erro de maneira organizada e fornece informações significativas para identificar e solucionar problemas rapidamente.

#### Subpasta "model-mocks"

A subpasta "model-mocks" é responsável por armazenar mocks de modelos de dados que são usados principalmente em ambientes de teste na camada de "Domain" e em outras camadas. Esses mocks definem respostas simuladas para métodos e funções que dependem de modelos de dados. Isso é particularmente valioso durante o desenvolvimento e execução de testes unitários, pois permite que controlemos os dados de entrada e saída de maneira previsível, garantindo que nossos testes sejam confiáveis e consistentes.

A pasta "entities" desempenha um papel importante em nossa camada de "Domain", fornecendo estruturas para lidar com exceções e facilitando a simulação de modelos de dados em ambientes de teste. Ela contribui para a confiabilidade e robustez de nossa aplicação, ao mesmo tempo que promove boas práticas de desenvolvimento e testes.

### Padrão para Pasta "model-mocks"

Dentro da pasta "entities", a subpasta "model-mocks" segue um padrão específico para criar mocks de modelos de entidades. Esses mocks são essenciais para definir respostas simuladas em ambientes de teste e em outras camadas da aplicação.

O padrão adotado é o seguinte:

- **Nome da Constante:** Cada arquivo dentro da pasta "model-mocks" deve exportar uma constante. O nome dessa constante segue um padrão consistente, começando com o nome da entidade seguido por "ModelMock." Isso garante uma convenção clara para identificar os mocks relacionados a uma entidade específica.

- **Tipo do Modelo:** O tipo da constante deve corresponder ao modelo de entidade ao qual se refere. Isso garante que os mocks sejam do mesmo tipo dos modelos de entidade que representam, contribuindo para a consistência e a precisão das respostas simuladas.

Seguindo esse padrão, facilitamos a criação e o uso de mocks de modelos de entidades em nossa aplicação, garantindo que eles estejam em conformidade com os modelos reais e sejam de fácil identificação.

Exemplo:

```typescript
import { UserModel } from '@/domain/models';
import { UsersRoleEnum } from '@/domain/shared/concerns/EnumTypes';

export const userModelMock: UserModel = {
  id: '70b7cf95-5295-4b54-9e4d-f5c31226c1e4',
  name: 'any_name',
  email: 'any_email',
  phone: '(99) 99999-9999',
  omie_code: 'any_omie_code',
  role: UsersRoleEnum.SUPER,
  password: '$2a$10$fHhN1WgZd.5NvfCkYF8HXu.J1sV1QXBQVUv3c8.y5yL.0K',
  updated_at: new Date('2022-09-19T12:11:16.209Z'),
  created_at: new Date('2021-07-22T00:01:41.029Z'),
  deleted_at: undefined,
};
```

## Pasta "models"

A pasta "models" desempenha um papel na organização dos modelos de entidades da nossa aplicação. Ela é responsável por abrigar os modelos de entidades que representam as principais estruturas de dados em nosso sistema. Cada modelo dentro desta pasta representa uma entidade do sistema, capturando os tipos de dados e a estrutura específica associados a essa entidade.

Esses modelos são essenciais para definir a forma como nossas entidades são representadas e manipuladas dentro da aplicação. Eles encapsulam os atributos e propriedades das entidades, garantindo que os dados sejam tratados de maneira consistente em toda a aplicação. Além disso, os modelos fornecem uma base sólida para as operações de leitura e gravação de dados, contribuindo para a integridade e a eficiência do sistema.

A pasta "models" promove uma abordagem organizada para gerenciar as estruturas de dados fundamentais em nossa camada de "Domain." Essa organização facilita a manutenção, a compreensão e a evolução de nossa aplicação, ao mesmo tempo em que contribui para a clareza e a consistência de nossos modelos de entidades.

### Padrão para Pasta "models"

Dentro da pasta "models", na camada de "Domain", seguimos um padrão específico para a definição dos tipos que representam as entidades de nosso sistema. Esse padrão é projetado para garantir a consistência entre os tipos e as entidades do banco de dados, abrangendo todas as propriedades e características.

O padrão adotado é o seguinte:

- **Exportação de Tipo com a Tag 'type':** Cada arquivo dentro da pasta "models" deve exportar um tipo utilizando a tag 'type'. Isso cria uma definição clara do tipo de entidade.

- **Nome do Tipo Baseado na Entidade:** O nome do tipo deve ser criado com base no nome da entidade que representa, seguido por "Model." Esse padrão permite uma associação direta entre o tipo e a entidade correspondente no banco de dados.

- **Correspondência com Entidades do Banco de Dados:** Os tipos definidos devem corresponder exatamente às entidades do banco de dados, incluindo todas as propriedades necessárias e opcionais. Isso abrange dados obrigatórios, opcionais, enums, strings, números e quaisquer outras propriedades que sejam parte da entidade.

Seguindo esse padrão, garantimos que nossos tipos de entidades na camada de "Domain" estejam em perfeita correspondência com as entidades do banco de dados, proporcionando uma representação precisa e consistente de nossos dados em toda a aplicação.

Exemplo:

```typescript
import { UsersRoleEnum } from '@/domain/shared/concerns/EnumTypes';

export type UserModel = {
  id: string;
  name: string;
  email: string;
  password: string;
  phone?: string;
  omie_code?: string;
  role: UsersRoleEnum;
  updated_at?: Date;
  created_at?: Date;
  deleted_at?: Date;
};
```

## Pasta "use-cases"

A pasta "use-cases" é o coração da nossa aplicação na camada de "Domain." Ela desempenha um papel vital ao implementar os contratos que definimos e, principalmente, é onde toda a regra de negócio da aplicação é concebida e executada.

Nesta pasta, encontramos a implementação concreta de nossos contratos de "use-case", o que significa que aqui é onde as operações mais críticas da aplicação são realizadas. Cada "use-case" é dedicado a uma tarefa específica e é responsável por orquestrar as operações necessárias para atingir um objetivo, como criar um usuário, listar fretes ou gerenciar um recurso.

Os "use-cases" não apenas aplicam as regras de negócio, mas também garantem que a aplicação opere de acordo com as políticas e diretrizes definidas, mantendo uma lógica centralizada e de fácil manutenção. Além disso, eles promovem a separação de preocupações, mantendo a camada de "Domain" desacoplada de detalhes de implementação específicos da infraestrutura.

A pasta de "use-cases" é verdadeiramente o epicentro das funcionalidades da nossa aplicação e é onde a magia acontece, transformando regras de negócio em funcionalidades concretas e valiosas para nossos usuários.

### Padrões para Use-Cases

Dentro da camada de "Domain", os "use-cases" desempenham um papel central na implementação das regras de negócio de nossa aplicação. Para garantir que nossos "use-cases" sigam um padrão consistente, adotamos as seguintes diretrizes:

1. **Exportação de Classe:** Cada "use-case" deve ser exportado como uma classe.

2. **Nome Baseado na Ação:** O nome da classe "use-case" deve refletir a ação que ela executará, seguindo o padrão do nome do contrato do "use-case." O nome deve ser descritivo e terminar com "UseCase."

3. **Implementação de Contrato:** Todas as classes de "use-case" devem implementar um contrato correspondente. Isso estabelece uma ligação clara entre o contrato e sua implementação.

4. **Injeção de Dependência:** Caso seja necessário usar outras classes dentro do "use-case", a injeção de dependência deve ser usada. Isso segue os princípios da arquitetura limpa e SOLID, garantindo o desacoplamento e a manutenibilidade do código.

5. **Método Público Único:** Cada classe "use-case" deve conter um único método público, responsável por realizar a ação principal. Além disso, podem existir métodos privados, desde que sejam únicos e executem apenas uma ação, com nomes descritivos.

6. **Uso da Tag 'public':** A tag 'public' deve ser usada em métodos públicos, garantindo a visibilidade correta.

7. **Bibliotecas Externas Injetadas:** Dentro dos "use-cases", e em qualquer outro arquivo na camada de "Domain", não devem ser utilizadas bibliotecas diretamente. Caso seja necessário o uso de bibliotecas externas, elas devem ser injetadas no construtor da classe, promovendo a manutenibilidade e evitando acoplamento desnecessário.

Seguindo esses padrões, nossos "use-cases" serão consistentes e seguirão as melhores práticas de desenvolvimento de software, contribuindo para uma aplicação robusta e de fácil manutenção.

Exemplo:

```typescript
import {
  ICreateUserRepository,
  IFindUserRepository,
} from '@/domain/contracts/repositories/users/user';
import { ICreateUserUseCase } from '@/domain/contracts/use-cases/users/user';
import { AlreadyExistsError } from '@/domain/errors/already-exists-error';
import { IEncrypter } from '@/domain/shared/concerns/encrypter';

export class CreateUserUseCase implements ICreateUserUseCase {
  constructor(
    private readonly userRepository: ICreateUserRepository &
      IFindUserRepository,
    private readonly encrypter: IEncrypter,
  ) {}

  public async execute(
    params: ICreateUserUseCase.Input,
  ): Promise<ICreateUserUseCase.Output> {
    const user = await this.userRepository.find({
      email: params.email,
    });
    if (user) {
      throw new AlreadyExistsError('user');
    }
    const hashedPass = await this.encrypter.encrypt(params.password);
    const newUser = await this.userRepository.create({
      ...params,
      password: hashedPass,
    });
    return newUser;
  }
}

```

# Infra Layer

A camada de "Infra" é um componente essencial de nossa arquitetura de software, projetada para lidar com aspectos técnicos e tecnológicos da aplicação. Ela atua como uma fronteira entre a camada de "Domain," onde residem as regras de negócio, e o mundo externo, abrangendo a interação com bibliotecas, serviços externos e recursos técnicos.

Nesta camada, concentramos nossos esforços em:

- **Integração Externa:** A camada de "Infra" é responsável por interagir com sistemas externos, como bancos de dados, serviços de terceiros e APIs. Isso inclui a gestão de conexões, transações e chamadas de rede, garantindo uma comunicação eficaz com recursos externos.

- **Detalhes Técnicos:** Aqui, lidamos com detalhes técnicos da aplicação, como a configuração de frameworks, manipulação de autenticação e autorização e gerenciamento de recursos de sistema.

- **Inversão de Dependência:** Seguindo o princípio da inversão de dependência, as classes na camada de "Infra" frequentemente implementam interfaces definidas na camada de "Domain." Isso permite que as classes na camada de "Domain" permaneçam desacopladas das implementações específicas de infraestrutura.

- **Frameworks e Bibliotecas:** Fazemos uso de frameworks e bibliotecas externas para implementar funcionalidades técnicas, como persistência de dados, segurança, comunicação em rede e muito mais. Isso nos permite aproveitar as melhores práticas e recursos da comunidade de desenvolvimento.

- **Testabilidade:** Mesmo tratando de detalhes técnicos, garantimos que a camada de "Infra" seja projetada de forma a ser testável. Isso envolve o uso de padrões de injeção de dependência, permitindo a substituição de implementações reais por simulações nos testes.

A camada de "Infra" é um componente flexível que nos permite adaptar nossa aplicação a diferentes tecnologias e plataformas, ao mesmo tempo em que mantém a camada de "Domain" focada nas regras de negócio. Ela desempenha um papel crucial na garantia de que nossa aplicação seja eficaz na integração com o mundo exterior e permaneça independente de detalhes técnicos.

## Estrutura de Pastas

```
infra/
    ├── database/
    │   ├── config/
    │   │   └── postgres/
    │   │       ├── typeorm/
    │   │       │   ├── migrations/ (migrations específicas para o PostgreSQL)
    │   │       │   └── utils/
    │   │       │       └── mocks/ (mocks específicos para PostgreSQL)
    ├── postgres/
    │   └── typeorm/
    │       ├── user/ (um exemplo de módulo com nome "user")
    │       │   ├── entities/ (entidades relacionadas ao módulo "user")
    │       │   └── repository/ (classes que implementam métodos de ações no banco de dados para "user")
    ├── gateways/ (bibliotecas usadas pelo sistema)
    └── protocols/ (classes com métodos de conexão a APIs externas)
```
