# Skill nestjs-best-practices
### Copiar el siguiente Prompt para crear el skill una vez ejecutado el comando $skill-creator:

```
1. Skill name: ‘nestjs-best-practices’
2. Create new Skill, description: que genere un proyecto con estructura NestJS usando módulos, controllers, services y providers, con inyección de dependencias, Prisma ORM y validación con Zod.
3. Location for skill folder: créalo dentro del directorio del proyecto ‘.agents/skills’
4. Specific Instructions:
   - usar NestJS v11.1.16 o version mas actualizada en https://www.npmjs.com/package/@nestjs/core
   - usar TypeScript
   - crear el proyecto con Nest CLI en estructura estándar
   - organizar la app por módulos o features
   - crear estructura base con modules, controllers, services, dto y prisma
   - usar Dependency Injection de Nest con providers e inyección por constructor
   - usar @Inject() cuando sea necesario inyectar tokens personalizados
   - usar Prisma ORM como capa de acceso a datos
   - usar SQLite como base de datos
   - incluir carpeta prisma con schema.prisma, datasource sqlite y generator client
   - crear PrismaService como provider reutilizable
   - controller: expone únicamente endpoints REST, valida entrada y delega a services
   - service: contiene lógica de negocio y acceso a datos mediante Prisma
   - usar Zod para validar datos definiendo esquemas y validando request body, params o query cuando corresponda
   - usar DTOs para request y response solo si ayudan a tipado y organización, pero priorizar esquemas Zod para validación
   - crear mapeo explícito entre DTO y modelo cuando sea necesario
   - usar decoradores REST de Nest como @Controller, @Get, @Post, @Patch, @Delete, @Param, @Body y @Query
   - no usar repository pattern clásico salvo necesidad real; preferir PrismaService o servicios específicos
   - cuando necesite iniciar la aplicación localmente, preferir npm run start:dev
   - registrar en AGENTS.md: Available skills y Skill trigger rules, si no existe lo creas
5. Activation Triggers: cuando el usuario pide crear una API básica para NestJS, o cuando pida crear, agregar o modificar un module, controller, service, dto, provider, PrismaService, schema Prisma, validaciones con Zod o endpoint REST.
