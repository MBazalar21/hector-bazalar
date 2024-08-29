# Ejercicio Técnico

Documentación del proyecto a presentar, cuyo fin es de describir el contenido e información

## Descripcion del Proyecto

La empresa XYZ Boutique tiene como actividad principal la venta de productos básicos. El Objetivo es controlar el abastecimiento del stock al momento de hacer los pedidos de productos.

## Conexion a la BD

Variables de entorno usadas para la conexion a la base de datos en el archivo .env

`DB_CONNECTION`  = mysql
`DB_HOST`  = localhost
`DB_DATABASE`  = delfostiDb
`DB_USERNAME`  = root
`DB_PASSWORD`  = root

#### Se almacenara la base de datos en la ruta (database/sql)

## Descripciones de APIS

Authorization Bearer Token : <TOKEN>
 
### Iniciar Sesion

```http
  GET /api/authentication/${usuario}/${contrasena}
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `usuario` | `string` | **Required**. Nombre del Usuario |
| `contrasena` | `string` | **Required**. Contraseña del Usuario |

### Registrar Usuario

```http
  POST /api/user/register
```
| Body | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `USUARIO` | `object` | **Required**. Objeto de Creación de Usuario |

Usuario:

```Object
  {
    cod_tra:autogenerado(USU000001),
    nombre:nombre del usuario,
    correo:correo electronico del usuario,
    telefono:telefono del usuario,
    puesto:puesto del usuario,
    rol_id:Identificador del rol asociado al usuario
  }
```

### Crear Pedido

```http
  POST /api/pedido/create
```

| Body | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `PEDIDO`      | `object` | **Required**. Objeto de Creación de Pedidos |


Pedido:

```Object
  {
    nro_ped:autogenerado(PED000001),
    fec_ped:fecha del pedido,
    usu_ven_id:Identificador del usuario vendedor,
    list_prod:[{
      prod_id: Identificador del producto,
      cantidad: Cantidad de producto,
      pre_tot: Precio total a cobrar por el producto
    }]
  }
```

- #### El pedido se crea en un estado Por Atender


### Cambiar Estado del Pedido

```http
  POST /api/pedido/change_state
```

| Body | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `CHANGESTATEPEDIDO`      | `object` | **Required**. Objeto de Cambio de estado de Pedidos |

ChangeStatePedido:

```Object
  {
    pedido_id:Identificador del pedido,
    est_ped_id:Identificador del estado
  }
```
- #### Si el pedido se cambia a un estado En Proceso y cambia la fecha de recepcion del pedido y el usuario repartidor asignado

- #### Si el pedido se cambia a un estado En Delivery y cambia la fecha de despacho

- #### Si el pedido se cambia a un estado Recibido y cambia la fecha de entrega