# Autoloader

As palavras-chave "DEVE", "NÃO DEVE", "OBRIGATÓRIO", "TEM QUE", "NÃO TEM QUE", "DEVERIA",
"NÃO DEVERIA", "RECOMENDADO", "PODE", and "OPCIONAL" devem ser interpretadas como
descrito no [RFC 2119](http://tools.ietf.org/html/rfc2119).

## 1. Visão geral

Esta PSR descreve a especificação para [autoloading][] classes de caminhos de
arquivo. É totalmente interoperável, e pode ser usada em adição a qualquer outra
especificaão de autoloader, incluindo [PSR-0][]. Esta PSR também descreve onde
colocar arquivos que serão carregados de acordo com a especificação.


## 2. Especificação

1. O termo "class" refere-se a classes, interfaces, traits, e outras estruturas
   similares.

2. Um nome de classe totalmente qualificado tem o seguinte formato:

        \<NamespaceName>(\<SubNamespaceNames>)*\<ClassName>

    1. O nome de classe totalmente qualificado DEVE ter um namespace
       de nível superior também conhecido como um "vendor namespace".

    2. O nome de classe totalmente qualificado PODE ter um ou mais sub-namespaces.
    
    3. O nome de classe totalmente qualificado DEVE ter um nome de classe de terminação.

    4. Sublinhados não tem significado especial em qualquer parte do nome de class
       totalmente qualificado.
    
    5. Caracteres do alfabeto no nome de classe totalmente qualificado PODEM
       ser qualquer combinação de minúsculos e maiúsculos.

    6. Todos nomes de classe DEVEM ser referenciados diferenciado maiúsculas e minúsculas.

3. Ao carregar um arquivo que corresponde a um nome de classe totalmente qualificado ...

    1. A justaposição de um ou mais namespaces principais ou sub-namespaces, 
       excluindo o separador de namespace principal, nos nomes de classe totalmente
       qualificados (um "prefixo de namespace") corresponde a pelo menos um "diretório base.

    2. Os sub-namespaces adjacentes após o "prefixo de namespace" corresponde
       a um sub-diretório dentro de um "diretório base", no qual os separadores
       de namespace representam separadores de diretório. O nome do sub-diretório
       DEVE coincidir no caso de sub-namespaces.

    3. A nome da classe de terminação corresponde ao nome do arquivo terminado em `.php`.
       O nome do arquivo DEVE coincidir com o nome da classe de terminação.

4. Autoloader implementations MUST NOT throw exceptions, MUST NOT raise errors
   of any level, and SHOULD NOT return a value.


## 3. Examples

The table below shows the corresponding file path for a given fully qualified
class name, namespace prefix, and base directory.

| Fully Qualified Class Name    | Namespace Prefix   | Base Directory           | Resulting File Path
| ----------------------------- |--------------------|--------------------------|-------------------------------------------
| \Acme\Log\Writer\File_Writer  | Acme\Log\Writer    | ./acme-log-writer/lib/   | ./acme-log-writer/lib/File_Writer.php
| \Aura\Web\Response\Status     | Aura\Web           | /path/to/aura-web/src/   | /path/to/aura-web/src/Response/Status.php
| \Symfony\Core\Request         | Symfony\Core       | ./vendor/Symfony/Core/   | ./vendor/Symfony/Core/Request.php
| \Zend\Acl                     | Zend               | /usr/includes/Zend/      | /usr/includes/Zend/Acl.php

For example implementations of autoloaders conforming to the specification,
please see the [examples file][]. Example implementations MUST NOT be regarded
as part of the specification and MAY change at any time.

[autoloading]: http://php.net/autoload
[PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[examples file]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader-examples.md
