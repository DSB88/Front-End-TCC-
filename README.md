# Front-End-TCC-
Repositório do front-end do trabalho de conclusão de curso 


import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.util.ArrayList;
import java.util.List;

public class RestTemplateUsageFinder {

    public static void main(String[] args) throws IOException {
        String projectRoot = "/caminho/do/seu/projeto"; // Substitua pelo caminho real do seu projeto
        List<String> restTemplateUsages = new ArrayList<>();

        findRestTemplateUsages(new File(projectRoot), restTemplateUsages);

        System.out.println("Chamadas RestTemplate encontradas em:");
        for (String usage : restTemplateUsages) {
            System.out.println(usage);
        }
    }

    private static void findRestTemplateUsages(File file, List<String> restTemplateUsages) throws IOException {
        if (file.isFile() && file.getName().endsWith(".java")) {
            String content = new String(Files.readAllBytes(file.toPath()));
            if (content.contains("RestTemplate")) {
                restTemplateUsages.add(file.getAbsolutePath());
            }
        } else if (file.isDirectory()) {
            File[] children = file.listFiles();
            if (children != null) {
                for (File child : children) {
                    findRestTemplateUsages(child, restTemplateUsages);
                }
            }
        }
    }
}
