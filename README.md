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
nova classse na Controller : NOME DA CLASSE :  AppDbContext
      public AppDbContext(DbContextOptions<AppDbContext> options) : base(options) { } 
 public DbSet <Categoria> Categoria { get; set; } 
 public DbSet <Lanche> lanche { get; set; }


adicionamis uma nova classe na Controller 

AppDbContext.class


program.cs 
builder.Services.AddDbContext<AppDbContext>(options =>
options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));


-- CODIGO COMPLETO -- 


using System.ComponentModel.DataAnnotations;
using System.ComponentModel.DataAnnotations.Schema;
using System.Globalization;
using System.Reflection;

namespace Projeto3ds.Models
{
    [Table("Lanche")]
    public class Lanche
    {
        [Key]
        public int LancheId { get; set; }

        // Virtual pois pertence a outra classe 

       // [ForeingKey]
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


using System.ComponentModel.DataAnnotations;
using System.ComponentModel.DataAnnotations.Schema;

namespace Projeto3ds.Models
{

    [Table("Categoria")]
    public class Categoria
    {
        [Key]
        public int CategoriaId { get; set; }

        public string CategoriaNome { get; set; }

        public string Descricao { get; set; }

        //Criando um lista para os tipos de lanche 
        // PROPRIEDADE DE NAVEGAÇÃO 
        public List <Lanche> Lanche { get; set; } 

    }
}

// pk = *
// 

(NOVA CLASSE) 
using Microsoft.EntityFrameworkCore;
using Projeto3ds.Models;

namespace Projeto3ds.Controllers
{
    public class AppDbContext:DbContext
    {
        // Programar
        //NÃO QUEBRAR ESSA LINHA DE JEITO NENHUM 
        // Essas classes serão mapeadas 
        public AppDbContext(DbContextOptions<AppDbContext> options) : base(options) { } 
        public DbSet <Categoria> Categoria { get; set; } 
        public DbSet <Lanche> lanche { get; set; }
         


    }
}


PROGRAM.CS


using Microsoft.EntityFrameworkCore;
using Projeto3ds.Controllers;


var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddControllersWithViews();

// lambida => para cortar o código
builder.Services.AddDbContext<AppDbContext>(options =>
options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));

var app = builder.Build();

// Configure the HTTP request pipeline.
if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Home/Error");
    // The default HSTS value is 30 days. You may want to change this for production scenarios, see https://aka.ms/aspnetcore-hsts.
    app.UseHsts();
}

app.UseHttpsRedirection();
app.UseStaticFiles();

app.UseRouting();

app.UseAuthorization();

app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");

app.Run();
