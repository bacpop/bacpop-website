---
title: "PopPUNK databases"
description: "Pre-built databases for use with PopPUNK"
featured_image: '/images/header8.jpg'
type: 'page'
---
{{< jquery >}}

Databases come in two flavours: *reference only*, or *all genomes*. Some also come
with external clusters (noted below) which give compatibility with existing schemes.
For larger databases you may wish to download using ftp for enhanced reliability/restarts
-- replace `http://` with `ftp://` in the links below and use your favourite client.

Typically, the reference only database will be sufficient for the main use case of assigning new samples to PopPUNK clusters, and updating the database with new clusters which have been found. The reference databases are usually significantly smaller.

For more detailed analyses, you may wish to download the all genomes database. If you wish to run either `poppunk-visualise` or any subclustering within strains this will require the full database.

In either case only the reference genomes will actually be used for query assignment, which does not change the results but gives a good speed up in program runtime.

See the [distributing models documentation page](https://poppunk.readthedocs.io/en/latest/model_distribution.html) for more details.

We welcome contributions for new species, or expansions of these databases [via our github](https://github.com/bacpop/PopPUNK/issues/new?assignees=johnlees&labels=enhancement&template=add-species-database.md&title=%5Bdatabase%5D).

{{< rawhtml >}}
<input type="text" id="search" size="50" placeholder="Type to search" title="Type in a name">
<table id="db-table" class="text-center align-middle">
  <tr class="header">
    <th width="28%" style="text-align:center">Species</th>
    <th width="5%" style="text-align:center;">Version</th>
    <th width="5%" style="text-align:center">Isolates</th>
    <th width="10%" style="text-align:center">Links</th>
    <th width="10%" style="text-align:center">References</th>
    <th width="10%" style="text-align:center">All</th>
    <th width="10%" style="text-align:center">External clusters</th>
  </tr>
  <tr>
    <td><i>Acinetobacter baumannii</i></td>
    <td style="text-align:center">v1</td>
    <td>8263</td>
    <td style="text-align:center"></td>
    <td style="text-align:center"><a href="http://ftp.ebi.ac.uk/pub/databases/pp_dbs/Acinetobacter_baumannii_v1_refs.tar.bz2">Download</a></td>
    <td style="text-align:center"><a href="http://ftp.ebi.ac.uk/pub/databases/pp_dbs/Acinetobacter_baumannii_v1_full.tar.bz2">Download</a></td>
    <td></td>
  </tr>
  <tr>
    <td><i>Bordetella pertussis</i></td>
    <td style="text-align:center">v1</td>
    <td>339</td>
    <td style="text-align:center"><a href="https://www.biorxiv.org/content/10.1101/2022.01.20.475763v1">Preprint</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Bordetella_pertussis_refs.tar.bz2">Download</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Bordetella_pertussis_full.tar.bz2">Download</a></td>
    <td></td>
  </tr>
    <tr>
    <td><i>Campylobacter jejuni</i></td>
    <td style="text-align:center">v1</td>
    <td>42453</td>
    <td style="text-align:center"><a href="https://www.ncbi.nlm.nih.gov/pathogens/">Portal</a></td>
    <td style="text-align:center">Coming soon</td>
    <td style="text-align:center"></td>
    <td></td>
  </tr>
  <tr>
    <td><i>Candida albicans</i></td>
    <td style="text-align:center">v1</td>
    <td></td>
    <td style="text-align:center"></td>
    <td style="text-align:center">Coming soon</td>
    <td style="text-align:center"></td>
    <td></td>
  </tr>
    <tr>
    <td><i>Enterococcus faecalis</i></td>
    <td style="text-align:center">v1</td>
    <td>2026</td>
    <td style="text-align:center"><a href="https://doi.org/10.1038/s41467-021-21749-5">Paper</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/enterococcus_faecalis_v1_refs.tar.bz2">Download</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/enterococcus_faecalis_v1_full.tar.bz2">Download</a></td>
    <td></td>
  </tr>
  <tr>
    <td><i>Enterococcus faecium</i></td>
    <td style="text-align:center">v2</td>
    <td>1658</td>
    <td style="text-align:center"><a href="https://www.nature.com/articles/s41564-020-00806-7">Paper</a></td>
    <td style="text-align:center"><a href="http://ftp.ebi.ac.uk/pub/databases/pp_dbs/Enterococcus_faecium_v2_refs.tar.bz2">Download</a></td>
    <td style="text-align:center"><a href="http://ftp.ebi.ac.uk/pub/databases/pp_dbs/Enterococcus_faecium_v2_full.tar.bz2">Download</a></td>
    <td></td>
  </tr>
  <tr>
    <td><i>Escherichia coli</i></td>
    <td style="text-align:center">v2</td>
    <td>30138</td>
    <td style="text-align:center"><a href="https://doi.org/10.1099/mgen.0.000499">Paper</a> & <a href="https://www.ncbi.nlm.nih.gov/pathogens/">Portal</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/enterococcus_faecium_v1_refs.tar.bz2">Download</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/escherichia_coli_v2_full.tar.bz2">Download</a></td>
    <td></td>
  </tr>
  <tr>
    <td><i>Haemophilus influenzae</i></td>
    <td style="text-align:center">v1</td>
    <td>89</td>
    <td style="text-align:center"><a href="https://doi.org/10.1073/pnas.1403353111">Paper</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Haemophilus_influenzae_v1_refs.tar.bz2">Download</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Haemophilus_influenzae_v1_full.tar.bz2">Download</a></td>
    <td></td>
  </tr>
    <tr>
    <td><i>Helicobacter pylori</i></td>
    <td style="text-align:center">v1</td>
    <td>2201</td>
    <td style="text-align:center"></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Helicobacter_pylori_v1_refs.tar.bz2">Download</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Helicobacter_pylori_v1_full.tar.bz2">Download</a></td>
    <td></td>
  </tr>
  <tr>
    <td>Influenza virus</td>
    <td style="text-align:center">v1</td>
    <td></td>
    <td style="text-align:center"></td>
    <td style="text-align:center">Coming soon</td>
    <td style="text-align:center"></td>
    <td></td>
  </tr>
    <tr>
    <td><i>Klebsiella pneumoniae</i></td>
    <td style="text-align:center">v3</td>
    <td>1361</td>
    <td style="text-align:center"><a href="https://doi.org/10.1038/s41564-019-0492-8">Paper</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Klebsiella_pneumoniae_v3_refs.tar.bz2">Download</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Klebsiella_pneumoniae_v3_full.tar.bz2">Download</a></td>
    <td></td>
  </tr>
  <tr>
    <td><i>Legionella pneumophila</i></td>
    <td style="text-align:center">v1</td>
    <td>3116</td>
    <td style="text-align:center"></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Legionella_pneumophila_v1_refs.tar.bz2">Download</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Legionella_pneumophila_v1_full.tar.bz2">Download</a></td>
    <td></td>
  </tr>
  <tr>
    <td><i>Listeria monocytogenes</i></td>
    <td style="text-align:center">v2</td>
    <td>40474</td>
    <td style="text-align:center"><a href="https://www.ncbi.nlm.nih.gov/pathogens/">Portal</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/listeria_monocytogenes_v2_refs.tar.bz2">Download</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/listeria_monocytogenes_v2_full.tar.bz2">Download</a></td>
    <td></td>
  </tr>
  <tr>
    <td><i>Mycobacterium abscessus</i></td>
    <td style="text-align:center">v1</td>
    <td>861</td>
    <td style="text-align:center"><a href="https://doi.org/10.1038/s41564-021-00963-3">Paper</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/mycobacterium_abscessus_v1_refs.tar.bz2">Download</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/mycobacterium_abscessus_v1.tar.bz2">Download</a></td>
    <td style="text-align:center">DCC</td>
  </tr>
  <tr>
    <td><i>Mycobacterium tuberculosis</i></td>
    <td style="text-align:center">v1</td>
    <td>13170</td>
    <td style="text-align:center"><a href="https://doi.org/10.1371/journal.pbio.3001421">Paper</a></td>
    <td style="text-align:center"><a href="http://ftp.ebi.ac.uk/pub/databases/pp_dbs/Mycobacterium_tuberculosis_v1_refs.tar.bz2">Download</a></td>
    <td style="text-align:center"><a href="http://ftp.ebi.ac.uk/pub/databases/pp_dbs/Mycobacterium_tuberculosis_v1_full.tar.bz2">Download</a></td>
    <td style="text-align:center">Lineage</td>
  </tr>
   <tr>
    <td><i>Neisseria gonorrhoeae</i></td>
    <td style="text-align:center">v1</td>
    <td>8801</td>
    <td style="text-align:center"><a href="https://doi.org/10.1371/journal.pbio.3001421">Paper</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Neisseria_gonorrhoeae_v1_refs.tar.bz2">Download</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Neisseria_gonorrhoeae_v1_full.tar.bz2">Download</a></td>
    <td></td>
  </tr>
  <tr>
    <td><i>Neisseria meningitidis</i></td>
    <td style="text-align:center">v1</td>
    <td>33379</td>
    <td style="text-align:center"><a href="https://doi.org/10.12688/wellcomeopenres.14826.1">Paper</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Neisseria_meningitidis_v1_refs.tar.bz2">Download</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Neisseria_meningitidis_v1_full.tar.bz2">Download</a></td>
    <td></td>
  </tr>
  <tr>
    <td><i>Pseudomonas aeruginosa</i></td>
    <td style="text-align:center">v1</td>
    <td>6082</td>
    <td style="text-align:center"><a href="https://doi.org/10.1371/journal.pbio.3001421">Paper</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Pseudomonas_aeruginosa_v1_refs.tar.bz2">Download</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Pseudomonas_aeruginosa_v1_full.tar.bz2">Download</a></td>
    <td></td>
  </tr>
  <tr>
    <td><i>Saccharomyces cerevisiae</i></td>
    <td style="text-align:center">v1</td>
    <td></td>
    <td style="text-align:center"></td>
    <td style="text-align:center">Coming soon</td>
    <td style="text-align:center"></td>
    <td></td>
  </tr>
    <tr>
    <td><i>Salmonella sp.</i></td>
    <td style="text-align:center">v1</td>
    <td>335647</td>
    <td style="text-align:center"></td>
    <td style="text-align:center">Coming soon</td>
    <td style="text-align:center"></td>
    <td></td>
  </tr>
  <tr>
    <td><i>Staphylococcus aureus</i></td>
    <td style="text-align:center">v1</td>
    <td>42117</td>
    <td style="text-align:center"><a href="https://staphopia.emory.edu/">Portal</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/staphylococcus_aureus_v1_refs.tar.bz2">Download</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/staphylococcus_aureus_v1_full.tar.bz2">Download</a></td>
    <td></td>
  </tr>
    <tr>
    <td><i>Stenotrophomonas maltophilia</i></td>
    <td style="text-align:center">v1</td>
    <td>1210</td>
    <td style="text-align:center"><a href="https://doi.org/10.1038/s41467-020-15123-0">Paper</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Stenotrophomonas_maltophilia_v1_refs.tar.bz2">Download</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Stenotrophomonas_maltophilia_v1_full.tar.bz2">Download</a></td>
    <td></td>
  </tr>
    <tr>
    <td><i>Streptococcus agalactiae</i></td>
    <td style="text-align:center">v1</td>
    <td>18029</td>
    <td style="text-align:center"><a href="https://doi.org/10.12688/wellcomeopenres.14826.1">Paper</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Streptococcus_agalactiae_v1_refs.tar.gz">Download</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Streptococcus_agalactiae_v1_full.tar.gz">Download</a></td>
    <td></td>
  </tr>
    <tr>
    <td><i>Streptococcus mitis</i></td>
    <td style="text-align:center">v1</td>
    <td>322</td>
    <td style="text-align:center"><a href="https://doi.org/10.1128/jcm.00802-22">Paper</a></td>
    <td style="text-align:center"></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Streptococcus_mitis_v1_full.tar.gz">Download</a></td>
    <td></td>
  </tr>
  <tr>
    <td><i>Streptococcus pneumoniae</i></td>
    <td style="text-align:center">v4</td>
    <td>42157</td>
    <td style="text-align:center"><a href="https://www.pneumogen.net/gps/">Website</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Streptococcus_pneumoniae_v4_ref.tar.bz2">Download</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Streptococcus_pneumoniae_v4_full.tar.bz2">Download</a></td>
    <td style="text-align:center">GPSC</td>
  </tr>
  <tr>
    <td><i>Streptococcus pyogenes</i></td>
    <td style="text-align:center">v1</td>
    <td>2084</td>
    <td style="text-align:center"><a href="https://doi.org/10.1038/s41588-019-0417-8">Paper</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Streptococcus_pneumoniae_v4_ref.tar.bz2">Download</a></td>
    <td style="text-align:center"><a href="https://ftp.ebi.ac.uk/pub/databases/pp_dbs/Streptococcus_pneumoniae_v4_full.tar.bz2">Download</a></td>
    <td></td>
  </tr>
</table>
</div>
<script>
$('#search').keyup(function() {

    var val = '^(?=.*\\b' + $.trim($(this).val()).split(/\s+/).join('\\b)(?=.*\\b') + ').*$',
        reg = RegExp(val, 'i'),
        text;


    $("#db-table tr").each(function (index) {
        if (!index) return;
        $(this).find("td").each(function () {
        text = $(this).text().replace(/\s+/g, ' ');
        var not_found = !reg.test(text);
        $(this).closest('tr').toggle(!not_found);
        return !reg.test(text);
        });
    });
});
</script>
{{< /rawhtml >}}
