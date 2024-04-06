Este es un proyecto en Next.js con el fin de explicar cómo desplegar una tienda con su respectiva base de datos desde vercel y poder hacer la reportería desde Grafana.


## Requerimientos:

- Tener instalado Node.js versión 18 o superior.
- Tener cuenta en GitHub
![1](docs/1.png)
- Tener cuenta en Vercel.com
- Tener cuenta en Grafana

## Pasos:
1. Forkear este repositorio en GitHub a tu propio repo de GitHub 
![2](docs/2.png)
![3](docs/3.png)

2. Crear una cuenta en Vercel.com
![4](docs/4.png)
![5](docs/5.png)
![6](docs/6.png)
![7](docs/7.png)
3. Conectar tu cuenta de Github a Vercel.com
![8](docs/8.png)
![9](docs/9.png)
4. Importar el Proyecto la-tienda a tu cuenta de Vercel
![10](docs/10.png)
5. No te preocupes, te va a dar un error cuando se te esté desplegando la aplicación.  :)
![11](docs/11.png)
![13](docs/13.png)
6. Ir a STORAGE y conectar una base de datos en POSTGRES
![14](docs/14.png)
![15](docs/15.png)
![16](docs/16.png)
![17](docs/17.png)
![18](docs/18.png)
7. Conectar el proyecto la-tienda a la base de datos de POSTGRES
![19](docs/19.png)
![20](docs/20.png)
8. Clonar el proyecto a tu computador local
![21](docs/21.png)
instalar git no es necesario si se usa linux
![22](docs/22.png)
```bash
git clone $URL
cd la-tienda
npm install
export POSTGRES_URL= $DATABASE
npx prisma migrate dev
npx prisma db seed
```

![n-25](docs/n-25.png)
![n-24](docs/n-24.png)
![n-23](docs/n-23.png)
![n-22](docs/n-22.png)

9. Volver a Vercel, a DEPLOYMENTS y re-deployar la aplicación
![n-21](docs/n-21.png)
![n-20](docs/n-20.png)
![n-18](docs/n-18.png)
10. Ahora en la aplicación se puede utilizar, tocando el boton VISIT.
![n-17](docs/n-17.png)
11. FELICITACIONES! Puedes probar la aplicación.

## Reportería con Grafana

1. Ir a Grafana y crearse una cuenta conectando tu cuenta de GitHub.
2. Instanciar un Grafana
3. Crear un datasource 
4. Agregar la configuración que venga desde el storage de Vercel
5. Crear Gráficos.

## Consultas de SQL 
Usuarios que han comprado en la tienda y sus monto total. 

```sql
select sum,social_name FROM (select  sum(price), sale_id from sales_details group by sale_id) as t1
JOIN sales on sales.id=t1.sale_id JOIN users on sales.user_id=users.id 
```

Nombre del usuario que más ha comprado.
```sql
select social_name FROM (select max(sum) 
FROM (select SUM(price*quantity) 
FROM sales_details JOIN sales on sales.id=sales_details.sale_id GROUP BY user_id) as t1) as t2 JOIN (select user_id,  SUM(price*quantity) 
FROM sales_details JOIN sales on sales.id=sales_details.sale_id GROUP BY user_id) as t3 on t3.sum=t2.max 
JOIN users on users.id=t3.user_id
```


---
Authors:
  - [Manuel Alba](https://github.com/elmalba)
  - [Laura Romero]([https://github.com/elmalba](https://github.com/lauraromero-cm)
  - [Lucas Abello]([https://github.com/elmalba](https://github.com/lexO-dat)
  - [Javier Oberto]([https://github.com/elmalba](https://github.com/Joberto14)
---

## License

[![CC0](http://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

Nuestros proyectos se construyen con la mentalidad de las aplicaciones de código abierto, utilizando la licencia MIT.
