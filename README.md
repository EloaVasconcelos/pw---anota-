    {
        public int LancheId { get; set; }

        // Virtual pois pertence a outra classe 
        public virtual Categoria CategoriaId { get; set; }

        public string DescrCurta { get; set; }

        public string DescrDetalhada { get; set; }

        public string Nome { get; set; }

        public string LanchePreferido { get; set; }

        // Virtual pois pertence a outra classe 
        // PROPRIEDADE DE NAVEGAÇÃO 
        public virtual Categoria Categoria { get; set; }

        public string ImgMini { get; set; }

        public string ImgUrl { get; set; }
        public decimal Preco { get; set; }
        public bool EmEstoque { get; set; }


    }

}


{
    public class Categoria
    {
        public int CategoriaId { get; set; }

        public string CategoriaNome { get; set; }

        public string Descricao { get; set; }

        //Criando um lista para os tipos de lanche 
        // PROPRIEDADE DE NAVEGAÇÃO 
        public List <Lanche> Lanche { get; set; } 

    }
}




##  AULA DO DIA 08/04

MANDEI NO TEAMS

## 09/04

adicionamis uma nova classe na Controller 

AppDbContext.class
