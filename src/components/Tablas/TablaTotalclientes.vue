<template>
  <div class="primary-container">
    <div class="secundary-container">
      <div class="items">
        <!-- Caja de búsqueda de cliente -->
        <input class="buscador" type="text" v-model="busqueda" placeholder="Buscar cliente...">

        <!-- Filtro por operario -->
        <select class="filtro" v-model="filtroOperario">
          <option value="">Todos los Operarios</option>
          <!-- Iteración sobre operarios únicos y selección de operario -->
          <option v-for="operario in operariosUnicos" :key="operario" :value="operario">{{ operario }}</option>
        </select>

        <!-- Botón de exportación de clientes -->
        <button @click="exportarClientes" class="btn-accion btn-exportar">Exportar Clientes</button>
      </div>

      <!-- Contenedor de la tabla -->
      <div class="table-container">
        <table class="table">
          <thead>
          <tr>
            <!-- Encabezados de tabla sin filtros por columna -->
            <th>Cliente N°</th>
            <th>Nombres y Apellidos</th>
            <th>Dirección</th>
            <th>Correo Electrónico</th>
            <th>Celular</th>
            <th>Identificación</th>
            <th>Número Identificación</th>
            <th>Estado Civil</th>
            <th>Ocupación</th>
            <th>Residencia</th>
            <th>Prefijo</th>
            <th>Empresa que Vende</th>
            <th>RUC Vendedor</th>
            <th>Dirección Vendedor</th>
            <th>Representante Legal Vendedor</th>
            <th>DNI Vendedor</th>
            <th>Nº Partida Poder Vendedor</th>
            <th>Moneda</th>
            <th>Número Cuenta</th>
            <th>CCI</th>
            <th>Fecha Entrega Proyecto</th>
            <th>Fecha Firma Contrato Definitivo</th>
            <th>Área Matriz (Has.)</th>
            <th>Registros de Partida Matriz</th>
            <th>Ubicación Lote (Predio Matriz)</th>
            <th>Unidad Catastral de Matriz</th>
            <th>Urbanización de Matriz</th>
            <th>Distrito de Matriz</th>
            <th>Provincia de Matriz</th>
            <th>Departamento de Matriz</th>
            <th>Compraventa de Matriz</th>
            <th>Situación Legal de Matriz</th>
            <th>Fecha Inicio Contrato</th>
            <th>Fecha Cancelación Contrato</th>
            <th>MZ (Cliente)</th>
            <th>LT (Cliente)</th>
            <th>Área en Letras (Cliente)</th>
            <th>Área Lote (Cliente)</th>
            <th>Cuota Ideal en Letras</th>
            <th>Cuota Ideal (Cliente)</th>
            <th>Por el Frente</th>
            <th>Por la Derecha</th>
            <th>Por la Izquierda</th>
            <th>Por el Fondo</th>
            <th>Nº Identif. (Cliente)</th>
            <th>Tipo Doc. (Cliente)</th>
            <th>Nombres y Apellidos (Cliente)</th>
            <th>Nacionalidad (Cliente)</th>
            <th>Estado Civil (Cliente)</th>
          </tr>
          </thead>
          <tbody>
          <tr v-for="(cliente, index) in clientesFiltrados" :key="cliente.ID_Cliente">
            <td>{{ index + 1 }}</td>
            <td>{{ cliente.nombresApellidos }}</td>
            <td>{{ cliente.direccion }}</td>
            <td>{{ cliente.correoElectronico }}</td>
            <td>{{ cliente.celularCliente }}</td>
            <td>{{ cliente.documentoIdentificacion }}</td>
            <td>{{ cliente.numeroIdentificacion }}</td>
            <td>{{ cliente.estadoCivil }}</td>
            <td>{{ cliente.ocupacion }}</td>
            <td>{{ cliente.residencia }}</td>
            <td>{{ cliente.prefijoPais }}</td>
            <td>{{ cliente.empresaVende }}</td>
            <td>{{ cliente.rucVendedor }}</td>
            <td>{{ cliente.direccionVendedor }}</td>
            <td>{{ cliente.representanteLegalVendedor }}</td>
            <td>{{ cliente.dniVendedor }}</td>
            <td>{{ cliente.numeroPartidaPoderVendedor }}</td>
            <td>{{ cliente.moneda }}</td>
            <td>{{ cliente.numeroCuenta }}</td>
            <td>{{ cliente.cci }}</td>
            <td>{{ cliente.fechaEntregaProyecto }}</td>
            <td>{{ cliente.fechaFirmaContrato }}</td>
            <td>{{ cliente.areaMatriz }}</td>
            <td>{{ cliente.registrosPartidaMatriz }}</td>
            <td>{{ cliente.ubicacionLoteMatriz }}</td>
            <td>{{ cliente.unidadCatastralMatriz }}</td>
            <td>{{ cliente.urbanizacionMatriz }}</td>
            <td>{{ cliente.distritoMatriz }}</td>
            <td>{{ cliente.provinciaMatriz }}</td>
            <td>{{ cliente.departamentoMatriz }}</td>
            <td>{{ cliente.compraventaMatriz }}</td>
            <td>{{ cliente.situacionLegalMatriz }}</td>
            <td>{{ cliente.fechaInicioContrato }}</td>
            <td>{{ cliente.fechaCancelacionContrato }}</td>
            <td>{{ cliente.mzCliente }}</td>
            <td>{{ cliente.ltCliente }}</td>
            <td>{{ cliente.areaLetrasCliente }}</td>
            <td>{{ cliente.areaLoteCliente }}</td>
            <td>{{ cliente.cuotaIdealLetras }}</td>
            <td>{{ cliente.cuotaIdealCliente }}</td>
            <td>{{ cliente.porFrente }}</td>
            <td>{{ cliente.porDerecha }}</td>
            <td>{{ cliente.porIzquierda }}</td>
            <td>{{ cliente.porFondo }}</td>
            <td>{{ cliente.numeroIdentifCliente }}</td>
            <td>{{ cliente.tipoDocCliente }}</td>
            <td>{{ cliente.nombresApellidosCliente }}</td>
            <td>{{ cliente.nacionalidadCliente }}</td>
            <td>{{ cliente.estadoCivilCliente }}</td>
            <!-- Botón de acción de editar -->
            <td class="acciones-td">
              <button @click="editarCliente(cliente.ID_Cliente)" class="btn-accion btn-editar">
                <i class="fas fa-edit"></i>
                <span class="accion-texto">Editar</span>
              </button>
            </td>
          </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>


<script>
import "@/assets/Tablas/Tablas.css";
import axios from 'axios';

export default {
  data() {
    return {
      clientes: [],  // Lista de todos los clientes
      busquedaGlobal: "",  // Campo de búsqueda global
      filtroOperario: "",  // Filtro por operario
      filtros: {
        nombre: "",
        nombresApellidos: "",
        direccion: "",
        correoElectronico: "",
        celularCliente: "",
        documentoIdentificacion: "",
        numeroIdentificacion: "",
        estadoCivil: "",
        ocupacion: "",
        residencia: "",
        prefijoPais: "",
      },
    };
  },
  computed: {
    // Computed property para filtrar los clientes según los valores de busqueda global, filtro por operario y filtros adicionales
    clientesFiltrados() {
      return this.clientes.filter(cliente => {
        const coincideBusqueda = Object.keys(cliente).some(key =>
            cliente[key] && cliente[key].toLowerCase().includes(this.busquedaGlobal.toLowerCase())
        );
        const coincideOperario = this.filtroOperario ? cliente.operario === this.filtroOperario : true;
        const coincideFiltros = Object.keys(this.filtros).every(key => {
          return cliente[key] && cliente[key].toLowerCase().includes(this.filtros[key].toLowerCase());
        });
        return coincideBusqueda && coincideOperario && coincideFiltros;
      });
    },
    // Computed property para obtener los operarios únicos (sin repetir)
    operariosUnicos() {
      return [...new Set(this.clientes.map(cliente => cliente.operario))];
    }
  },
  mounted() {
    this.obtenerClientes();
  },
  methods: {
    // Método para obtener los clientes desde el backend (API)
    async obtenerClientes() {
      try {
        const userData = JSON.parse(localStorage.getItem("user"));
        const idOperario = userData?.idOperario;

        if (!idOperario) {
          console.error("No se encontró 'idOperario' en localStorage.");
          alert("No se pudo obtener el ID del operario.");
          return;
        }

        const response = await axios.get("http://localhost:8080/api/clientes/operario", {
          headers: {
            "Content-Type": "application/json",
            "X-User-ID": idOperario,
          },
          withCredentials: true,
        });

        this.clientes = response.data;
      } catch (error) {
        console.error("Error al obtener clientes:", error);
        alert("Hubo un error al obtener los clientes.");
      }
    },
    // Método para redirigir a la página de edición del cliente
    editarCliente(idCliente) {
      this.$router.push({ name: 'EditarCliente', params: { id: idCliente } });
    },
    // Método para exportar los clientes a un archivo CSV
    exportarClientes() {
      const headers = ["Cliente N°", "Nombres y Apellidos", "Dirección", "Correo Electrónico", "Celular", "Identificación", "Número Identificación", "Estado Civil", "Ocupación", "Residencia", "Prefijo"];
      const rows = this.clientes.map(cliente => [
        `"${cliente.ID_Cliente}"`,
        `"${cliente.nombresApellidos}"`,
        `"${cliente.direccion}"`,
        `"${cliente.correoElectronico}"`,
        `"${cliente.celularCliente}"`,
        `"${cliente.documentoIdentificacion}"`,
        `"${cliente.numeroIdentificacion}"`,
        `"${cliente.estadoCivil}"`,
        `"${cliente.ocupacion}"`,
        `"${cliente.residencia}"`,
        `"${cliente.prefijoPais}"`,
        `"${cliente.empresaVende}"`,
        `"${cliente.rucVendedor}"`,
        `"${cliente.direccionVendedor}"`,
        `"${cliente.representanteLegalVendedor}"`,
        `"${cliente.dniVendedor}"`,
        `"${cliente.numeroPartidaPoderVendedor}"`,
        `"${cliente.moneda}"`,
        `"${cliente.numeroCuenta}"`,
        `"${cliente.cci}"`,
        `"${cliente.fechaEntregaProyecto}"`,
        `"${cliente.fechaFirmaContrato}"`,
        `"${cliente.areaMatriz}"`,
        `"${cliente.registrosPartidaMatriz}"`,
        `"${cliente.ubicacionLoteMatriz}"`,
        `"${cliente.unidadCatastralMatriz}"`,
        `"${cliente.urbanizacionMatriz}"`,
        `"${cliente.distritoMatriz}"`,
        `"${cliente.provinciaMatriz}"`,
        `"${cliente.departamentoMatriz}"`,
        `"${cliente.compraventaMatriz}"`,
        `"${cliente.situacionLegalMatriz}"`,
        `"${cliente.fechaInicioContrato}"`,
        `"${cliente.fechaCancelacionContrato}"`,
        `"${cliente.mzCliente}"`,
        `"${cliente.ltCliente}"`,
        `"${cliente.areaLetrasCliente}"`,
        `"${cliente.areaLoteCliente}"`,
        `"${cliente.cuotaIdealLetras}"`,
        `"${cliente.cuotaIdealCliente}"`,
        `"${cliente.porFrente}"`,
        `"${cliente.porDerecha}"`,
        `"${cliente.porIzquierda}"`,
        `"${cliente.porFondo}"`,
        `"${cliente.numeroIdentifCliente}"`,
        `"${cliente.tipoDocCliente}"`,
        `"${cliente.nombresApellidosCliente}"`,
        `"${cliente.nacionalidadCliente}"`,
        `"${cliente.estadoCivilCliente}"`
      ]);

      // Construcción del CSV y agregando la cabecera
      let csvContent = "data:text/csv;charset=utf-8," + headers.join(",") + "\n";
      rows.forEach(row => {
        csvContent += row.join(",") + "\n";
      });
      // Creación del enlace para descargar el archivo CSV
      const encodedUri = encodeURI(csvContent);
      const link = document.createElement("a");
      link.setAttribute("href", encodedUri);
      link.setAttribute("download", "clientes.csv");
      document.body.appendChild(link);
      link.click();
    }
  }
};
</script>


<style scoped>
/* Aquí tu CSS si necesitas más personalización */
</style>
