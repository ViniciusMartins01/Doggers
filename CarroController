// Importações e instâncias necessárias
import Crud from '../mvc/Crud.js';
import express from 'express';
import path from 'path';
import { fileURLToPath } from 'url';
import bodyParser from 'body-parser';

// Necessário para obter __dirname em ES Modules
const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);

const app = express();
const router = express.Router();
const crud = new Crud(); // Instância da classe Crud

app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());

app.use(express.static(path.join(__dirname, '../../pages/public')));

// Rota para a página de exclusão (apagar.html)
app.get('/apagar', function (req, res) {
  res.sendFile(path.join(__dirname, '../../pages/public/apagar.html'));
});

// Rota para apagar um carro pelo ID
app.delete('/apagar/:id', function (req, res) {
  const { id } = req.params;
  
  crud.delete(id, function (resultado) {
    res.json({ message: 'Carro deletado com sucesso!', id, resultado });
  });
});

// Rota para a página de seleção (selecionar.html)
app.get('/selecionar', function (req, res) {
  res.sendFile(path.join(__dirname, '../../pages/public/selecionar.html'));
});

// Rota para selecionar todos os carros ou por ID
app.get('/selecionar/:id?', function (req, res) {
  const { id } = req.params;

  if (id) {
    crud.selectById(id, function (carro) {
      res.json(carro);
    });
  } else {
    crud.selectAll(function (carros) {
      res.json(carros);
    });
  }
});

// Atualizar o CRUD para corrigir o SQL da função delete
crud.delete = function (id, callback) {
  let sql = "DELETE FROM carro WHERE id = ?";
  // Supondo que você já tenha um método que execute consultas SQL
  this.run(sql, [id], callback);
};

// Iniciar o servidor
let server = app.listen(3000, function () {
  let host = server.address().address;
  let port = server.address().port;
  console.log("Servidor iniciado em http://%s:%s", host, port);
});
