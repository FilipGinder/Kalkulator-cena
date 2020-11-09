<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <script src="https://code.jquery.com/jquery-3.4.1.min.js"></script>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css" integrity="sha384-9aIt2nRpC12Uk9gS9baDl411NQApFmC26EwAOH8WgZl5MYYxFfc+NcPb1dKGj7Sk" crossorigin="anonymous">
    <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js" integrity="sha384-Q6E9RHvbIyZFJoft+2mJbHaEWldlvI9IOYy5n3zV9zzTtmI3UksdQRVvoxMfooAo" crossorigin="anonymous"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/js/bootstrap.min.js" integrity="sha384-OgVRvuATP1z7JjHLkuOU7Xw704+h835Lr+6QL9UvYjZE3Ipu6Tp75j7Bh/kR0JKI" crossorigin="anonymous"></script>
    <script src="//code.jquery.com/ui/1.12.1/jquery-ui.js"></script> <!--  DODATAK ZA VIBRACIJU INPUTA PRILIKOM PRAZNOG POLJA-->
    <meta charset="utf-8">
    <title></title>
    <style media="screen">
    body{
      background-color: purple;
    }
    #levi_div{
      background-color: purple;
      color: white;
    }
    #srednji_div{
      margin-top: 5px;
      background-color: orange;
    }
    #desni_div{
      background-color: purple;
      color: white;
    }
      .prvi_div{
        background-color: white;
        border: 1px solid black;
        padding: 20px 20px 20px 20px;
      }
      h2{
        text-align: center;
      }
      .drugi_div{
        background-color: white;
        margin-top: 5px;
        border: 1px solid black;
        padding: 20px 20px 20px 20px;
        margin-bottom: 10px;
      }
      #izracunaj{
        width: 100%;
      }
      #umanji{
        width: 100%;
      }
      #ispis_umenjenja{
        width: 100%;
      }
      #ponisti{
        width: 100%;
      }
      #ispis{
        width: 100%;
      }
      #zeljeni_broj{
        width: 100%;
      }
      #zeljeni_pdv{
        width: 100%;
      }
      #odaberi_procenat{
        width: 100%;
      }
      #prikaz_umanjen{
        width: 100%;
      }
    </style>
    <script type="text/javascript">
      $(document).ready(function(){
         $("#zeljeni_pdv").keyup(function(){
           $("#ponisti").attr("disabled", false);
          var jedino_broj = /^[0-9]*$/;
          if(!jedino_broj.test($("#zeljeni_pdv").val())){
            alert('U ovo polje je obavezno uneti samo broj od 1 do 99 u zavisnosti od zeljenog PVD-a');
            $("#zeljeni_pdv").val('');
          }
        });
        $("#odaberi_procenat").keyup(function(){
         var jedino_broj = /^[0-9]*$/;
         if(!jedino_broj.test($("#odaberi_procenat").val())){
           alert('U ovo polje je obavezno uneti samo broj od 1 do 99 u zavisnosti od zeljenog procenta umanjenja');
           $("#odaberi_procenat").val('');
         }
       });
        $("#zeljeni_broj").keyup(function(){
          $("#ponisti").attr("disabled", false);
            var jedino_broj = /^[0-9]*$/;
            if(!jedino_broj.test($("#zeljeni_broj").val())){
              alert('U ovo polje je obavezno uneti samo broj');
              $("#zeljeni_broj").val('');
            }
        })
        $("#izracunaj").click(function(){
          if($("#zeljeni_broj").val() == "")
          {
            $( "#zeljeni_broj" ).effect( "shake" );
        //    alert("Prvo unesite broj za koji zelite da racunate proporcionalnu umanjenost za odredjeni PDV");
            return;
          }
          else
          {
            a = $("#zeljeni_broj").val();
            b = $("#zeljeni_pdv").val();
            c = a / ( parseInt(100) + parseInt(b)) * 100;
           $("#ispis").val(c);
           $("#ispis").css("border", "2px solid red");
           $("#odaberi_procenat").attr("disabled", false);
           $("#zeljeni_broj").attr("disabled", true);
           $("#zeljeni_pdv").attr("disabled", true);
           $("#umanji").attr("disabled", false);
           $("#izracunaj").attr("disabled", true);
          }
        });
         $("#umanji").click(function(){
           if($("#odaberi_procenat").val() == "")
           {
             $( "#odaberi_procenat" ).effect( "shake" );
            // alert("Unesite procenat za koji zelite da umanjite br. za koji racunate");
             return;
           }
           else
           {
               procenat_umanjenja = $("#odaberi_procenat").val();
               x = a / 100;
               x = x * procenat_umanjenja;
               y = a - x;
               t = y / ( parseInt(100) + parseInt(b)) * 100;
               $("#prikaz_umanjen").val(t);
               $("#ispis_umenjenja").val(y);
               $("#prikaz_umanjen").css("border", "2px solid red");
               $("#odaberi_procenat").attr("disabled", true);
               $("#umanji").attr("disabled", true);
               $("#izracunaj").attr("disabled", true);
           }
         });
        $("#ponisti").click(function(){
          $("#zeljeni_broj").val('');
          $("#ispis").val('');
          $("#odaberi_procenat").val('');
          $("#prikaz_umanjen").val('');
          $("#ispis_umenjenja").val('');
          $("#odaberi_procenat").attr("disabled", true);
          $("#zeljeni_broj").attr("disabled", false);
          $("#zeljeni_pdv").attr("disabled", false);
          $("#umanji").attr("disabled", true);
          $("#ponisti").attr("disabled", true);
          $("#izracunaj").attr("disabled", false);
          // $("#umanji").attr("disabled", false);
          $("#ispis").css("border", "1px solid lightgray");
          $("#prikaz_umanjen").css("border", "1px solid lightgray");
        })
      });
    </script>
  </head>
  <body>
 <div class="container">
   <div class="row">
     <div class="col-md-2" id="levi_div">
        <h5>Osnovna namena kalkulatora</h5>
        <p>Osnovna i jedina namena kalkulatora je racunanje potrebne srazmerno umanjene cifre za odredjeni PDV. <br><br>
        Primer : <br> Ukoliko uzmemo br 5000 za racunanje i 20% PDV, uz pomoc ovog kalkulatora cemo dobiti broj<b> 4166.666666666666</b> koji kada bi se uvecao za 20% dobili bi tacno 5000.</p>
     </div>
     <div class="col-md-8" id="srednji_div">
            <h2>Kalkulator unosa cena</h2>
            <div class="prvi_div">
              <div class="row">
                <div class="col-md-6">
                  <label for="zeljeni_broj">Unesite BR za racunanje:</label><br>
                  <input type="text" id="zeljeni_broj" placeholder="Unesite zeljeni broj">
                </div>
                <div class="col-md-6">
                  <label for="zeljeni_pdv">Unesite PDV:</label><br>
                  <input type="text" id="zeljeni_pdv" maxlength="2" value="20" title="Odaberite zeljeni procenat od 1% do 99%">
                </div>
              </div>
              <br>
              <label for="ispis">Rezultat koji kada se uveca za zeljeni PDV ispada kao br. za koji smo racunali:</label>
              <input type="text" id="ispis" disabled placeholder="Rezultat" >
              <br><br>
              <input type="button" id="izracunaj" class="btn btn-success" value="Izracunaj">
            </div>
            <div class="drugi_div">
              <h3>Ne obavezno racunanje</h3>
                <div class="row">
                  <div class="col-md-6">
                    <label for="odaberi_procenat">Odaberi procenat (%) za koji zelis umanjiti br.za koji se racuna:</label>
                    <input type="text" id="odaberi_procenat" maxlength="2" placeholder="Odaberi umanjenje za odredjeni procenat" disabled>
                  </div>
                  <div class="col-md-6">
                    <label for="ispis_umenjenja"><br> Umanjenje za zeljeni broj: <br> </label>
                    <input type="text" id="ispis_umenjenja" disabled>
                  </div>
                </div>
                <br>
                <div class="row">
                  <div class="col-md-12">
                    <label for="prikaz_umanjen">Rezultat srazmerno umanjen za PDV i procenat umanjenja:</label>
                    <input type="text" id="prikaz_umanjen" placeholder="Rezultat" disabled>
                  </div>
                </div>
                   <br>
              <input type="button" id="umanji" disabled class="btn btn-warning" value="Umanji">
              <br><br>
              <input type="button" id="ponisti" disabled class="btn btn-danger" value="Ponisti sve">
            </div>
     </div>
     <div class="col-md-2" id="desni_div">
        <h5>Drugi deo kalkulatora</h5>
        <p>Za zeljenu cenu je moguce odmah izracunati i umanjenje za odredjeni procenat. <br><br> Primer :<br> Za zeljeni broj 5000 uz 20 PDV-a i npr. <b>25% umanjenja</b> cemo dobiti broj 3125 koji kada bi uvecali za 20% PDV-a dobili bi 3750 sto je umanjenje od 25% u odnosu na zeljeni broj 5000.<br></p>
     </div>
   </div>
 </div>
  </body>
</html>
